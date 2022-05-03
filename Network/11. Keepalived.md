# Failover with Keepalived

## Khái niệm keepalived ?
Keepalived là 1 chương trình dịch vụ tạo độ sẵn sàng cao (High Availability) cho hệ thống dịch vụ và khả năng cân bằng tải (Load Balancing) đơn giản. Sức mạnh chủ yếu ở dịch vụ High Availability IP Failover là chính do sự gọn nhẹ, tối ưu trong dịch vụ. 
Keepalived cung cấp các thư viện (Framework) cho 2 chức năng chính là Health Checking (Load Balancing) và VRRP (High Availability).

## Cấu trúc keepalived 
Để đảm bảo tính mạnh mẽ và ổn định, Keepalive được chia thành 3 process riêng biệt. Hai child process tương ứng với mỗi chức năng chính của keepalive. Parent process được sử dụng để thực thi một khung giám sát gọi là watchdog. Watchdog sẽ định kỳ "hỏi thăm" các tiến trình con và khởi động lại nếu không thấy chúng phản hồi.

````
PID         111     Keepalived  <-- Parent process monitoring children
            112     \_ Keepalived   <-- VRRP child
            113     \_ Keepalived   <-- Healthchecking child
````

Keepalived sử dụng 4 kernel linux chính: LVS Framework, Netfilter Framework, Netlink Interface, Multicast.

![image](https://user-images.githubusercontent.com/79156398/165438206-f57468df-b913-4017-86ff-57a02d648d51.png) 

Cấu trúc chi tiết hơn: 
![image](https://user-images.githubusercontent.com/79156398/165438468-466f371b-3856-42c7-b2e8-fb49c7ee6e98.png)



## Load balancing 
Cân bằng tải sử dụng framework IPVS của Linux module kernel. IPVS (IP Virtual Server) thực hiện cân bằng tải lớp transport-layer trong nhân Linux, được biết đến với tên gọi khác là Layer-4 switching. 

### Các thuật toán lập lịch của IPVS

#### Round Robin
Round Robin là thuật toán cho phép dữ liệu gửi vòng tròn lần lượt giữa các máy chủ. Việc này khiến cho lưu lượng chia đều tới các máy chủ.

#### Weighted Round Robin
Weighted Round Robin là thuật toán cho phép gửi dữ liệu giống như Round Robin. Nhưng bổ sung thêm phần trọng số. Các máy chủ có trọng số cao hơn được xoay vòng nhiều hơn.

#### Least Connection
Là thuật toán lập lịch động. Nó tính các kết nối trực tiếp cho từng máy chủ và phân phối dữ liệu tới các máy có số kết nối được thiết lập ít nhất. Nó không thể cân bằng tải giữa các máy chủ có khả năng xử lý khác nhau do trạng thái TIME_WAIT của giao thức TCP.

#### Weighted Least Connection
Là thuật toán lập lịch động giống như Least Connection nhưng mỗi máy chủ có thêm một trọng số. Các máy chủ có trọng số cao hơn sẽ nhận được phần trăm số kết nối nhiều hơn. Giá trị trọng số mặc định là 1.

#### Locality-Based Least Connection
Là thuật toán cân bằng tải dựa trên IP đích. Thường được sử dụng trong cache cluster. IP đích sẽ được phân bổ cho máy chủ của nó. Nếu nó quá tải. Weighted Least Connection sẽ được sử dụng.

#### Locality-Based Least Connection with Replication
Là thuật toán cân bằng tải dựa trên IP đích. Thường được sử dụng trong cache cluster. IP đích sẽ được phân bổ cho một cụm máy chủ, cụ thể là máy chủ có ít kết nối nhất(least-connection). Nếu cả cụm máy chủ đều over loaded. Nó chọn là máy chủ có ít kết nối nhất trong tất cả các máy chủ còn lại bên ngoài và thêm nó vào cụm. Nếu nhóm máy chủ chưa được sửa đổi trong thời gian đã chỉ định, thì nút được tải nhiều nhất sẽ bị xóa khỏi nhóm máy chủ. In order to avoid high degree of replication.

#### Destination Hashing
Thuật toán lập lịch băm đích chỉ định các kết nối mạng đến các máy chủ thông qua việc tra cứu bảng băm được gán tĩnh theo địa chỉ IP đích của chúng.

#### Source Hashing
Thuật toán lập lịch băm nguồn chỉ định các kết nối mạng đến các máy chủ thông qua việc tra cứu bảng băm được gán tĩnh theo địa chỉ IP nguồn của chúng.

#### Shortest Expected Delay
Là thuật toán lập lịch chỉ định các kết nối mạng đến máy chủ với độ trễ dự kiến ​​ngắn nhất. 

Độ trễ dự kiến là ``(Ci+1)/Ui`` với : 
- `i` server thứ `i` được gửi qua.

- `Ci` số kết nối qua server thứ `i`.

- `Ui` fixed service rate (weight) của server thứ i.

#### Never Queue

Là thuật toán lập lịch sử dụng mô hình [two-speed model](empty). Khi có sẵn một máy chủ nhàn rỗi, công việc sẽ được gửi đến máy chủ không hoạt động, thay vì chờ đợi một máy chủ nhanh. Hay nói cách khác, cứ máy chủ nào rảnh là nó gửi. Nếu không có máy chủ nào rảnh, nó sẽ dùng thuật toán Shortest Expected Delay.

#### Overflow-Connection

Thuật toán thực hiện cân bằng tải "overflow" theo số kết nối đang hoạt động. Nó sẽ giữ tất cả các node hiện tại đang có trọng số cao nhất và tràn sang các node có trọng số nhỏ hơn trong trường hợp các kết nối vượt quá trọng số của máy chủ hiện tại. Thuật toán này không phù hợp với giao thức UDP.

### LVS 
![image](https://user-images.githubusercontent.com/79156398/165429118-c033fab9-8457-4a4e-826e-d866a6ba12fd.png)

**Linux Virtual Server (LVS)** chỉ một nhóm server gồm có các Load Balancer (LB) và các Real Server. Nhóm này sẽ có 1 Virtual IP duy nhất (VIP) cho phép các máy bên ngoài tạo request tới. Khi lưu lượng đến từ internet, tất cả dữ liệu có đích là VIP nên sẽ trỏ về máy có VIP đó - Load Balancer. Việc phân phối dữ liệu trả về client tùy thuộc vào cách cấu hình LVS. Thường có 3 loại như sau:

- NAT: Các Real Server với Private IP sẽ được NAT thông qua 1 VIP ở LB Server. LB Server sẽ đóng vai trò như là Gateway của hệ thống cân bằng tải. Các Real Server sẽ trỏ Gateway tới LB Server. Mọi dữ liệu đều phải đi qua LB Server. Mô hình này có một vấn đề là dẽ gây bottleneck.
- Direct Routing (DSR): Mô hình này khác với mô hình dùng NAT ở chỗ các dữ liệu trả về Client sẽ được gửi trực tiếp từ máy Real Server. Các Real Server sẽ tự động đổi địa chỉ nguồn của gói tin trả về thành địa chỉ VIP. Mô hình này giải quyết vấn đề bottleneck. Hạn chế của mô hình này là các máy Real Server cần phải đặt chung một mạng cục bộ.
- IP Tunneling: Mô hình này cũng giống mô hình dùng DSR nhưng khác ở chỗ các máy Real Server có thể ở các mạng cục bộ khác nhau. Chúng sẽ tương tác với Real Server thông qua IP tunnel. Mô hình này giải quyết hạn chế về vị trí của các máy chủ Real Server.

## High Availability

**High Availability** hay *Tính sẵn sàng cao* là việc cung cấp khả năng chịu lỗi cho máy chủ nhằm tăng tính dự phòng cho các dịch vụ. Tính dự phòng được tạo nên bằng cách gom nhóm các máy chủ chạy các dịch vụ giống nhau. Keepalived triển khai sử dụng giao thức VRRP (Virtual Router Redundancy Protocol) cho phép điều hướng chịu lỗi. 
Keepalived sẽ gom nhóm các máy chủ lại và trao 1 Virtual IP cùng 1 địa chỉ MAC tương ứng (trong một vài môi trường mạng, nếu cần). Các máy chủ dịch vụ sử dụng chung VIP phải liên lạc với nhau bằng địa chỉ multicast 224.0.0.18 bằng giao thức VRRP. Các máy chủ sẽ có độ ưu tiên (priority) trong khoảng từ 1 – 254, và máy chủ nào có độ ưu tiên cao nhất sẽ thành Master, các máy chủ còn lại sẽ thành các Slave/Backup, hoạt động ở chế độ chờ. - Các BACKUP sẽ bầu ra 1 MASTER mới khi MASTER quá hạn gửi các gói tin quảng bá. Khi MASTER cũ hoạt động bình thường trở lại thì server này có thể lại trở thành MASTER hoặc trở thành BACKUP tùy theo cấu hình độ ưu tiên của các router.

## Cấu hình sử dụng Keepalived 

Keepalive hoạt động dựa trên các thông số trên file cấu hình. Đường dẫn file cấu hình của Keepalive trên Ubuntu: ``/etc/keepalived/keepalived.conf`` 

<a name="4.1"></a>
### 4.1 Global definitions

``` sh
global_defs {
  notification_email {
    email
    email
  }
  notification_email_from email
  smtp_server host
  smtp_connect_timeout num
  lvs_id string
}
```

- `global_defs` : cho biết đây là block cấu hình của global def
- `notification_email` : email nhận được thông báo
- `notification_email_from` : email được sử dụng khi xử lí câu lệnh “MAIL FROM:” SMTP
- `smtp_server` : SMTP server dùng để gửi mail thông báo
- `smtp_connection_timeout` : timeout cho tiến trình xử lí SMTP

<a name="4.2"></a>
### 4.2 Virtual server definitions

``` sh
virtual_server (@IP PORT)|(fwmark num) {
    delay_loop num
    lb_algo rr|wrr|lc|wlc|sh|dh|lblc
    lb_kind NAT|DR|TUN
    (nat_mask @IP)
    persistence_timeout num
    persistence_granularity @IP
    virtualhost string
    protocol TCP|UDP

    sorry_server @IP PORT

    real_server @IP PORT {
      weight num
      TCP_CHECK {
        connect_port num
        connect_timeout num
      }
    }
    real_server @IP PORT {
      weight num
      MISC_CHECK {
        misc_path /path_to_script/script.sh
        (or misc_path “/path_to_script/script.sh <arg_list>”)
      }
    }
    real_server @IP PORT {
        weight num
        HTTP_GET|SSL_GET {
            url { # You can add multiple url block
              path alphanum
              digest alphanum
            }
            connect_port num
            connect_timeout num
            nb_get_retry num
            delay_before_retry num
        }
    }
}
```

- `delay_loop` : số giây giữa các lần check
- `lb_algo` : load balancing algorithm (rr|wrr|lc|wlc…)
- `lb_kind` : method dùng để forwarding (NAT|DR|TUN)
- `persistence_timeout` : thời gian timeout cho các persistence connection
- `Virtualhost` : HTTP virtualhost để dùng cho  HTTP|SSL_GET
- `protocol` :  (TCP|UDP)
- `sorry_server` : server được add vào pool nếu mọi server đều bị down
- `Weight` : trọng số cho load balancing
- `TCP_CHECK` : check bằng tcp connect
- `MISC_CHECK` : check bằng user defined script
- `misc_path` : Đường dẫn tới script
- `HTTP_GET` : check bằng HTTP GET request
- `SSL_GET` : check bằng SSL GET request

<a name="4.3"></a>
### 4.3 VRRP Instance definitions

``` sh
vrrp_sync_group string {
  group {
    string
    string
  }
  notify_master /path_to_script/script_master.sh
      (or notify_master “/path_to_script/script_master.sh <arg_list>”)
  notify_backup /path_to_script/script_backup.sh
      (or notify_backup “/path_to_script/script_backup.sh <arg_list>”)
  notify_fault /path_to_script/script_fault.sh
      (or notify_fault “/path_to_script/script_fault.sh <arg_list>”)
}
vrrp_instance string {
  state MASTER|BACKUP
  interface string
  mcast_src_ip @IP
  lvs_sync_daemon_interface string
  virtual_router_id num
  priority num
  advert_int num
  smtp_alert
  authentication {
    auth_type PASS|AH
    auth_pass string
  }
  virtual_ipaddress { # Block limited to 20 IP addresses
    @IP
    @IP
    @IP
  }
  virtual_ipaddress_excluded { # Unlimited IP addresses number
    @IP
    @IP
    @IP
  }
  notify_master /path_to_script/script_master.sh
    (or notify_master “/path_to_script/script_master.sh <arg_list>”)
  notify_backup /path_to_script/script_backup.sh
    (or notify_backup “/path_to_script/script_backup.sh <arg_list>”)
  notify_fault /path_to_script/script_fault.sh
    (or notify_fault “/path_to_script/script_fault.sh <arg_list>”)
}
```

- `State` : trạng thái của Instance
- `Interface` : Interface mà Instance đang chạy
- `mcast_src_ip` : địa chỉ Multicast
- `lvs_sync_daemon_inteface` : Interface cho LVS sync_daemon
- `Virtual_router_id` :  VRRP router id
- `Priority` : thứ tự ưu tiên trong VRRP router
- `advert_int` : số  advertisement interval trong 1 giây
- `smtp_aler` : kích hoạt thông báo SMTP cho MASTER
- `authentication` :  VRRP authentication
- `virtual_ipaddress` : VRRP VIP
