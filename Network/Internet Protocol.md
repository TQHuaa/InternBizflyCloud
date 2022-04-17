
# Giao thức IP Protocol 
**Giao thức IP(Internet Protocol)** là một giao thức thuộc chồng giao thức TCP/IP. Nếu tham chiếu theo mô hình TCP/IP, giao thức IP sẽ nằm ở tầng 3, tầng Internet. Là **giao thức hướng dữ liệu**, chúng sử dụng một địa chỉ logic gọi là **địa chỉ IP** (IP Address). Mỗi thiết bị trong mạng sẽ được cấp 1 địa chỉ IP. Các máy tính trong mạng sẽ truyền thông, giao tiếp với nhau bằng cách sử dụng địa chỉ IP đó để định danh máy chủ nguồn và máy chủ đích. Nếu coi các thiết bị trong mạng internet giống như là các người dùng, trong trường hợp giả sử như mọi người liên lạc với nhau qua thư tay, thì IP có thể so sánh như địa chỉ nhà của họ. Các địa chỉ này sẽ gisup cho các nhân viên bưu tá có thể biết được đâu là điểm đến của bức thư, cũng như đâu là nơi gửi. Việc này giúp cho các hai người có thể gửi ở bất cứ đơn vị giao vận thư tín nào. Tương tự, sử dụng IP giúp cho các thiết bị có thể dễ dàng gửi dữ liệu đi mà không cần phải thiết lập một đường kết nối có sẵn. Hiện nay có hai phiên bản của giao thức IP đang được sử dụng là IPv4 và IPv6.

## IPv4
**IPv4  hay Internet Protocol version 4, hoặc giao thức IP thế hệ thứ 4** là loại phổ biến và đã sử dụng từ thuở đầu. Giao thức IPv4 có một số đặc điểm sau: 
-   Là 1 trong những giao thức quan trọng nhất của bộ giao thức TPC/IP.
-   Là giao thức hướng không liên kết (connectionless): dữ liệu của IP được truyền đi ngay lập tức nếu có thể (best effort), không có bất kì cơ chế thiết lập kết nối , không có cơ chế báo nhận hay điều khiển luồng nào được sử dụng với IP, các gói tin IP cũng không được đánh số thứ tự khi trao đổi trên mạng…
-   Mỗi gói tin IP được xử lý một cách hoàn toàn độc lập với các gói tin IP khác .
-   Giao thức IP sử dụng cơ chế định địa chỉ theo kiểu phân cấp, trong đó phần NetworkID của địa chỉ giống như tên của một con đường và phần hostID của địa chỉ sẽ là số nhà của một căn nhà trên con đường ấy.
-   Không có cơ chế khôi phục lại gói tin bị mất trên đường truyền. Việc này được giao lại cho các giao thức tầng trên để đảm bảo độ tin cậy (TCP).

Header của IP được định nghĩa trong tài liệu RFC 791. 

![IPv4_Packet-en svg](https://user-images.githubusercontent.com/79156398/163294717-ca8a8db4-3e97-46af-b426-944532a76f28.png)

Trong đó: 
-   **VERS (4 bit)**: chỉ ra phiên bản hiện hành của IP đang được dùng, Nếu trường này khác với phiên bản IP của thiết bị nhận, thiết bị nhận sẽ từ chối và loại bỏ các gói tin này.

-   **HLEN (IP Header Length - 4 bit):**  chỉ độ dài phần tiêu đề của datagram, tính theo đơn vị word (32 bits). Nếu không có trường này thì độ dài mặc định của header là 5 từ.

-   **Service Type (8 bit)**: đánh dấu dữ liệu (marking) phục vụ cho tác vụ QoS với các gói tin IP.

-   **Precedence (3 bit)**: chỉ thị quyền ưu tiên gửi datagram, cụ thể:

|Priority| Main|
| ----- | ------ |
| 111 | Network Control (cao nhất) |
| 011 | flash |
| 110 | Internetwork Control |
| 010 | Immediate |
| 101 | CRITIC/ECP |
| 001 | Priority |
| 100 | Flas Override |
| 000 | Routine (thấp nhất) |

-   **Delay (1 bit)**  : chỉ độ trễ yêu cầu.  _0_: độ trễ bình thường;  _1_: độ trễ thấp
    
-   **Throughput (1 bit)**  : chỉ số thông lượng yêu cầu.  _0_: thông lượng bình thường;  _1_: thông lượng cao
    
-   **Reliability (1 bit)**: chỉ độ tin cậy yêu cầu.  _0_: độ tin cậy bình thường;  _1_: độ tin cậy cao
    
-   **Total Length (16 bit)**: chiều dài của toàn bộ gói tin IP kể cả phần header được tính theo byte. Để biết chiều dài của dữ liệu cần lấy tổng chiều dài này trừ đi HLEN.
    
-   **Identification (16 bit)**: Trường định danh, cùng các tham số khác như địa chỉ nguồn (Source address) và địa chỉ đích (Destination address) để định danh duy nhất cho mỗi Datagram được gửi đi bởi 1 trạm. Thông thường phần định danh được tăng thêm 1 khi 1 Datagram được gửi đi.
    
-   **Flags (3 bit)**: Cờ sử dụng trong khi phân đoạn các Datagram.
    
    -   Bit 0: reserved chưa sử dụng, giá trị luôn là 0.
    -   Bit 1:  _DF = 1_: Gói tin bị phân đoạn, có nhiều hơn 1 đoạn,  _DF = 0_: Gói tin ko bị phân đoạn.
    -   Bit 2:  _MF = 0:_  đoạn cuối cùng,  _MF = 1_: chưa là đoạn cuối cùng, còn đoạn khác phía sau nữa.

-   **Fragment Offset (13 bit):**  Chỉ vị trí của đoạn phân mảnh (Fragment) trong IP Datagram tính theo đơn vị 64 Bit.
    
-   **Time to Live (TTL) (8 bit)**: sử dụng để chống loop gói tin IP khi xảy ra lỗi định tuyến trên sơ đồ mạng. Giá trị này được đặt lúc bắt đầu gửi gói tin và nó sẽ giảm đi 1 đơn vị khi đi qua 1 router. Khi TTL = 0, gói tin sẽ bị loại bỏ.
    
-   **Protocol (8 bit)**: nhận dạng giao thức nào đang được truyền tải trong phần data của gói tin IP, như TCP hay UDP.
    
-   **Header checksum (8 bit)**: kiểm tra lỗi của IP Header. Nếu như việc kiểm tra này thất bại, gói dữ liệu sẽ bị huỷ bỏ tại nơi xác định được lỗi.
    
-   **Source Address (32 bit)**: địa chỉ của trạm nguồn.
    
-   **Destination Address (32 bit)**: địa chỉ của trạm đích.
    
-   **Option (có độ dài thay đổi)**: cho phép thêm vào tính năng mới cho giao thức IP.
    
-   **Padding (độ dài thay đổi)**: Cấu trúc của gói IP quy định option phải là bội số của 32 bit nên nếu option không đủ số bit , các bit padding sẽ được thêm vào để đạt được yêu cầu này .
    
-   **Data (độ dài thay đổi)**: vùng dữ liệu có độ dài là bội của 8 bit, tối đa là 65535 byte.

Địa chỉ IP được đề cập ở trường header. Chúng có độ dài 32 bit. Để dễ viết và hiển thị, 32 bit được chia thành 4 cụm 8 bit, gọi là các octet. Các octet được biểu diễn dưới dạng số thập phân phân tách bởi dấu chấm. Khi sử dụng, chúng lại được chia tiếp thành 2 phần: Network và host. Phần network là phần cố định tượng trưng cho 1 mạng, phần host là phần được dùng để chia cho các máy tính sử dụng trong mạng đó. 

![ViDuIP](https://user-images.githubusercontent.com/79156398/163294787-167fdb65-9cfa-4d01-a39e-bff3944c2ba1.png)

### Subnet mask 

Để phân biệt giữa phần network và phần host trong địa chỉ IP. Subnet mask được sử dụng. Subnet mask biểu thị số bit được sử dụng làm phần network. Cứ mỗi bit trong phần network sẽ tương ứng với bit 1 trong phần subnet mask. Phần còn lại là hostID với bit 0. Như vậy, subnet mask cũng có độ dài 32 bit với 4 octet. Với ví dụ trên, trong địa chỉ IP mẫu, ta thấy phần network chiếm 16 bit nên subnet mask là 1111 1111. 1111 1111. 0000 0000. 0000 0000 (tương đương với 255.255.0.0). Ngoài ra, ta có thể sử dụng ký hiệu `/` cùng với số lượng bit phần networkID ở sau địa chỉ IP. Ví dụ: 131.108.122.204/16

### Gateway, Broadcast address, Network address

**Gateway** là một máy tính hoặc một thiết bị định tuyến như router, switch sử dụng để quản lý các máy host trong một mạng. Tất cả các dữ liệu từ host sẽ phải đi qua gateway để xử lý bằng cách định tuyến,..
**Địa chỉ quảng bá**  hay **Broadcast address** thường được sử dụng khi gateway muốn gửi các gói tin broadcast - gói tin đến tất cả các host trong mạng mà gateway quản lý. Địa chỉ quảng bá có tất cả các bit phần hostID là 1.
**Địa chỉ mạng** hay **Network address** dùng để định danh cho một mạng. Địa chỉ mạng có tất cả các bit phần hostID là 0.

### Các lớp địa chỉ

Không gian địa chỉ IP được chia thành các lớp như sau:

![các lớp địa chỉ ](https://user-images.githubusercontent.com/79156398/163294998-3d08ccf6-521e-449b-b84d-ce38ae6b9f7c.png)

#### Lớp A

-   Địa chỉ lớp A sử dụng một otet(8 bit) đầu làm phần mạng, ba octet sau làm phần host
-   Bit đầu của một địa chỉ lớp A luôn được giữ là  _**0**_.
-   Các địa chỉ lớp mạng của lớp A gồm :  _**1.0.0.0 -> 126.0.0.0**_.
-   Mạng  _**127.0.0.0**_  được sử dụng làm  _**loopback**_
-   Phần host có 24 bit => mỗi mạng lớp A có (_**2^24 – 2**_) host.

#### Lớp B

-   Địa chỉ lớp B sử dụng hai octet đầu làm phần mạng , hai octet sau làm phần host.
-   Hai bit đầu của một địa chỉ lớp B luôn được giữ là  _**1 0**_
-   Các địa chỉ mạng lớp B gồm :  _**128.0.0.0 -> 191.255.0.0**_  . Có tất cả  _**2^14=16384**_  mạng trong lớp B.
-   Phần host dài 16 bit => một mạng lớp B có (_**2^16 – 2 = 65534**_) host.

#### Lớp C

-   Địa chỉ lớp C sử dụng 3 octet đầu làm phần mạng , một octet sau làm phần host.
-   Ba bit đầu của một địa chỉ lớp C luôn được giữ là  _**1 1 0**_.
-   Các địa chỉ mạng lớp C gồm :  _**192.0.0.0 -> 223.255.255.0**_. Có tất cả  _**2^21**_  mạng trong lớp C.
-   Phần host dài 8 bit do đó có một mạng lớp C có (_**28 – 2 = 254**_) host.

#### Lớp D

-   Bốn bit đầu của một địa chỉ lớp D luôn được giữ là  _**1 1 1 0**_
-   Gồm các địa chỉ thuộc dải:  _**244.0.0.0 -> 239.255.255.255**_
-   Được sử dụng để làm địa chỉ  _**multicast**_.

#### Lớp E

-   Năm bit đầu của một địa chỉ lớp E luôn được giữ là  _**1 1 1 1**_
-   Địa chỉ thuộc dải từ  _**240.0.0.0**_  trở đi
-   Được sử dụng cho mục đích dự phòng.

**Chú ý:**

-   Các lớp địa chỉ IP có thể sử dụng để đặt cho các host là các lớp A,B,C
-   Để dễ dàng nhận diện một địa chỉ IP thuộc lớp nào , ta có thể quan sát octet đầu của địa chỉ nằm trong khoảng giá trị:

|Địa chỉ lớp|Octet đầu của địa chỉ|
|--|--|
|A|1 -> 126|
|B|128 -> 191|
|C|192 -> 223|
|D|224 -> 239|
|E|240 -> 255|

Tuy nhiên việc phân chia cứng thành các lớp (A, B, C, D, E) làm hạn chế việc sử dụng toàn bộ không gian địa chỉ dẫn đến lãng phí không gian địa chỉ. Vậy giải pháp là gì 🤔?  

Đó chính là IP Public, IP Private.

### Địa chỉ IP Public, IP Private
**Public IP** là địa chỉ được **ISP** (nhà cung cấp dịch vụ Internet) cấp và có thế được "nhìn thấy" và truy cập từ Internet. Giống như địa chỉ nhà dùng để nhận thư tín, bưu phẩm vậy. Mỗi public IP chỉ tồn tại độc nhất trên mạng Internet cho cả toàn cầu, vì đó không thể tồn tại hai thiết bị (server, máy tính, router,...) có cùng địa chỉ public IP.

**Private IP** là các địa chỉ được cấp phát bởi InterNIC cho phép các công ty, tổ chức có thể tạo cho họ một mạng cục bộ riêng. Có ba dãy IP ở class A, class B và class C được IANA (Tổ chức cấp phát số hiệu trên Internet) dành riêng để đánh địa chỉ private IP.

|Lớp|Dải địa chỉ|Số host|
|---|---|--|
|A|10,0.0.0 đến 10.255.255.255|16777216|
|B|172.16.0.0 đến 172.31.255.255|1048576|
|C|192.168.0.0 đến 192.168.255.255|65536|

### Các hạn chế của IPv4

Hai hạn chế lớn nhất của IPv4 chính là bảo mật và sự thiếu hụt địa chỉ. Ở thời điểm mới được tạo ra vào thế kỷ trước. IPv4 chỉ được chú trọng vào việc thiết lập kết nối, bỏ qua bảo mật. Khối lượng địa chỉ với 32 bit, tương đương khoảng 4 tỉ địa chỉ là vô cùng thoải mái vào thời điểm đó với số ít các phòng nghiên cứu, cơ quan quân sự kết nối tới. Nhưng với tốc độ phát triển chóng mặt, số lượng các thiết bị mạng tăng vọt. Sự bùng nổ Internet đến thời điểm hiện tại khiến cho tài nguyên Ipv4 được sử dụng gần như là cạn kiện. Chính vì những hạn chế như vậy. Các nhà nghiên cứu đã cho ra đời giao thức IP thế hệ mới. IPv6!

## IPv6

**IPv6 hay Internet Protocol version 6** là phiên bản phổ biến thứ 2 sau IPv4. Nó được coi là tương lai của giao thức IP khi mà trong hoàn cảnh IPv4 nảy sinh nhiều hạn chế. Mà tại sao lại không phải là IPv5? Điều gì đã xảy ra với IPv5? Lý do chính mà IPv5 bị loại bỏ là do nó cũng sử dụng 32 bit để biểu diễn địa chỉ - nhược điểm lớn nhất của IPv4. IPv6 có tới 128 bit biểu diễn địa chỉ, tức là một số lượng địa chỉ IP rất lớn lên tới ~340 x 10^36. Đây là một con số mà ở thời điểm hiện tại thì nó gần như là vô hạn. 

![image](https://user-images.githubusercontent.com/79156398/163725133-ab808f1a-ab5f-40e7-895b-7501a3eb249c.png)

Cấu trúc Frame của IPv6 cũng có một số thay đổi so với IPv4. Lưu ý rằng tiêu đề IPv6 có ít trường hơn, điều này làm cho nó hiệu quả hơn và xử lý nhanh hơn. Một ưu điểm lớn khác là độ dài tiêu đề là kích thước cố định 40 byte, so với kích thước độ dài thay đổi của tiêu đề IPv4.

Trong đó : 

- **Version** :
Trường **Version** là số nhận dạng phiên bản của giao thức IP. Nó được đặt thành 4-bit trong IPv4 và 6-bit trong IPv6.
- **Traffic Class** : Thực hiện chức năng tương tự trường "Service Type" của địa chỉ IPv4. Trường này được sử dụng để biểu diễn mức ưu tiên của gói tin. Node gửi gói tin cần thiết lập giá trị phân loại độ ưu tiên nhất định cho gói tin IPv6, sử dụng trường Traffic Class.
- **Flow Label** : Trường Flow Label sử dụng để định danh một dòng dữ liệu giữa nguồn và đích. Flow Label được sử dụng trong IPv6 sẽ hỗ trợ tốt hơn thực thi QoS.
> Khái niệm Flow : 
- **Payload Length** : Độ dài Payload
- **Next Header** : Tương tự trường Protocol trong IPv4.

Một số giá trị phổ biến nhất được hiển thị trong bảng dưới đây.

| Giá trị Next Header (bằng hex) | Giao thức |
| -- | -- |
|6|TCP|
|11|UDP|
|2F|GRE|
|32|ESP|
|3A|ICMPv6|
|3B|None|
|59|OSPF|

- **Hop Limit** : Tương tự trường **Time to Live** trong IPv4
- **Source Address** : Địa chỉ nguồn
- **Destination Address**: Địa chỉ đích

### Biểu diễn địa chỉ IPv6

Địa chỉ IPv6 dài 128 bit, được chia làm 8 nhóm, mỗi nhóm gồm 16 bit, được ngăn cách với nhau bằng dấu hai chấm “:”. Mỗi nhóm được biểu diễn bằng 4 số hexa. Ví dụ: 
~~~
FEDC:BA98:768A:0C98:FEBA:CB87:7678:1111  
1080:0000:0000:0070:0000:0989:CB45:345F
~~~

![image](https://user-images.githubusercontent.com/79156398/163725101-13e9ea14-6f80-4c12-813a-23c8e8a54e8d.png)

8 octet chia làm 3 phần: 3+1+4 (Siteprefix + Subnet ID + Interface ID)

### Quy tắc viết rút gọn

Những địa chỉ IPv6 lớn, khả năng cung cấp địa chỉ cho nhiều node và cung cấp cấu trúc phân cấp linh hoạt, nhưng nó không dễ để viết ra. Vì vậy cần có 1 số nguyên tắc để nhằm rút ngắn lại cách biểu diễn địa chỉ IPv6. Sau đây là các quy tắc để rút gọn IPv6:  

- Cho phép bỏ các số 0 nằm trước mỗi nhóm (octet).  
- Thay bằng số 0 cho nhóm có toàn số 0.  
- Thay bằng dấu ``::`` cho các nhóm liên tiếp nhau có toàn số 0.

Ví dụ về nén địa chỉ IPv6:  
Cho một địa chỉ: ``1080:0000:0000:0070:0000:0989:CB45:345F``
Dựa theo các quy tắc đã nêu trên, có thể nén địa chỉ IP trên như sau: ``1080::70:0:989:CB45:345F`` hoặc ``1080:0:0:70::989: CB45:345F``

Chú ý: Dấu ``::`` chỉ sử dụng đƣợc 1 lần trong toàn bộ địa chỉ IPv6 (nhiều dấu ``::`` có thể gây ra sự nhầm lẫn hoặc không thể biết đúng vị trí của các octet trong địa chỉ IPv6).

### Biểu diễn của Address Prefixes

Prefix của địa chỉ IPv6 được biểu diễn tương tự với kí hiệu IPv4 CIDR. IPv6 prefix được biểu diễn như sau: ``**IPv6-address/prefix-length**``

Trong đó,**IPv6-address** là bất kì địa chỉ có giá trị, **Prefix-length** là số bit liền kề nhau được bao gồm trong prefix.

Ví dụ: Sau đây là quy tắc biểu diễn cho 56 bit prefix 
``200F00000000AB:`` 
``200F::AB00:0:0:0:0/56``  
``200F:0:0:AB00::/56``

Chú ý với địa chỉ IPv6, kí hiệu ``::`` được sử dụng 1 lần duy nhất trong mỗi sự biểu diễn. Điều quan trọng nên phải nói lần 2.

Theo sau là các cách biểu diễn sai của 56 bit prefix:  
``200F:0:0:AB/56``
``200F::AB00/56``
``200F::AB/56``

Cách biểu diễn đầu tiên là không hợp lệ bởi vì các số 0 theo sau trong vòng một trường 16-bit (``AB00``) bị mất, và địa chỉ không đủ chiều dài hợp lệ. Địa chỉ IPv6 trên bên trái của dấu gạch chéo ``/`` phải là một địa chỉ IPv6 có chiều dài đầy đủ hoặc được nén hợp lệ. Cách biểu diễn thứ hai và thứ ba là địa chỉ IPv6 được nén hợp lệ nhưng nó không giãn ra thành địa chỉ chính xác. Thay vì ``200F:0000:0000:AB00:0000:0000:0000:0000`` nó sẽ giãn thành ``200F:0000:0000:0000:0000:0000:0000:AB00`` và ``200F:0000: 0000:0000:0000:0000:0000:00AB`` tương ứng.

### Phân loại địa chỉ IPv6

Có 3 loại địa chỉ IPv6 :

- **Unicast**
- **Multicast**
- **Broadcast**

### Lợi thế của IPv6

Do thiết kế, IPv6 sẽ mang lại cho ta những lợi ích sau: 
- Loại bỏ hoàn toàn giao thức NAT.
- Khôi phục lại nguyên lý kết nối end-end của internet.
- Tăng dung lượng địa chỉ IP.
- Cấu trúc định tuyến tốt hơn do IPV6 được thiết kế hoàn toàn phân cấp.
- Quản trị TCP/IP tốt hơn do không cần DHCP và các cấu hình thủ công.
- Hỗ trợ bảo mật tốt hơn.

---> Giảm độ phức tạp, tăng tính bảo mật.
 
 Trên đây là một số kiến thức về giao thức **Internet Protocol** mà mình đã tổng hợp. Cảm ơn các bạn đã đọc bài và hãy ``Pull request`` nếu bài viết có lỗi gì nhé!
