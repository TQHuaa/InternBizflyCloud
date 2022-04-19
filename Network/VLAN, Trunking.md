
VLAN, VLAN Trunking, va VTP
#VLAN

## VLAN là gì ?
VLAN là kỹ thuật chuyển mạch của lớp 2 và định tuyến của lớp 3 để có thể giới hạn miền đụng độ và miền quảng bá. Về bản chất, việc chia VLAN sẽ khiến cho mạng LAN ban đầu có nhiều miền quảng bá nhỏ. Các host trong các miền quảng bá khác nhau nếu muốn liên lạc với nhau thì cần phải được định tuyến. VLAN có thể cấu hình trên router, trên 1 hoặc nhiều switch. 

Ví dụ: từ một switch 24 cổng ta chia 6 cổng cho phòng nhân sự, 6 cổng cho phòng kế toán, 12 cổng cho phòng dev.

VLAN đáp ứng nhiều yếu tố: 
- Tăng tính bảo mật.
- Tiết kiệm, tránh lãng phí khi chỉ cần một switch có thể tạo nhiều VLAN.
- Tiết kiệm băng thông.

![image](https://user-images.githubusercontent.com/79156398/163938599-c1144db4-b825-4008-b766-996d9b935c0e.png)

## Cấu hình VLAN

### Tạo VLAN bằng lệnh
``SW(config)#vlan n``
> n thuộc 0 – 4095. Trong đó:
- VLAN 0 và 4095: không được sử dụng(đã fix vào IOS ko được sử dụng)
- VLAN 1 : VLAN default
- VLAN 2 – 1001: Normal range(có thể sử dụng được)
- VLAN 1002 đến 1005 : VLAN default, dùng để kết nối với các hệ thống mạng khác như : FDDI, token Ring …(không kết nối được system Ethernet)
- VLAN 1006 – 4094 : VLAN extended range( dùng cho các Switch Transparent)

### Gán port vào VLAN
``Switch(config)#interface f0/1``
Chuyển SW về mode access(mode access dùng để kết nối các end user)
``Switch(config-if)#switchport mode access``
Gán các port vào VLAN của mình
``Switch(config-if)#switchport access vlan n``

### Gán 1 range port vào VLAN

````
Switch(config)#interface range f0/1-8
Switch(config-if)#switchport mode access
Switch(config-if)#switchport access vlan n
````

### Đặt tên cho VLAN (các VLAN default thì ko đặt tên được)

````
Switch(config)#vlan 2
Switch(config-vlan)#name sale
````
	
## Cấu hình subinterface trên Cisco

![image](https://user-images.githubusercontent.com/79156398/163938893-d70a02fe-0707-4b2c-a883-3d84369fc81e.png)

**Subinterface** là việc chia nhỏ 1 interface trên router và switch(của cisco) ra thành nhiều interface (cổng luận lý) nhỏ hơn. Kỹ thuật chia sub interface trên được gọi là kỹ thuật InterVLAN routing(kỹ thuật định tuyến giữa các VLAN). Ta có thể tạo 2 tỷ cổng luận lý. Thông thường ta tạo khoảng 3-4 cổng luận lý cho mỗi VLAN(khi tạo nhiều thì mạng sẽ chậm vì nó chia bandwith cho từng cổng luận lý tương ứng với mỗi VLAN. 

### Các lệnh cấu hình subinterface

Chia một interface ra các interface nhỏ, ví dụ:

``Router(config-if)#interface f0/1.n``

Vào mode sub-interface để tạo IP:

````
Router(config-subif)#encapsulation dot1Q n
Router(config-subif)#ip address 192.168.1.254 255.255.255.0
Router(config-subif)#no shutdown
````

# VLAN Trunking

## VLAN Trunking là gì ? 

![image](https://user-images.githubusercontent.com/79156398/163939050-c90ad596-7e6d-4c65-b132-e9a716022263.png)

VLAN Trunking là việc tạo một đường truyền mà trên đường truyền đó có dữ liệu của nhiều VLAN khác nhau đi qua. Việc tạo VLAN có tác dụng tiết kiệm chi phí, hoặc trong trường hợp ta chỉ có một đường truyền vật lý để cho các vlan đi qua. Có 2 chuẩn Trunking :

- IEEE: 802.1q(dot1q) : Đây là khung đóng gói trunking theo chuẩn quốc tế. Chuẩn này sẽ thêm 4 bytes giá trị 802.1q tags vào phần header của khung Ethernet.

![image](https://user-images.githubusercontent.com/79156398/163939188-08d4431d-9f28-4971-a683-fe72b11846e7.png)

- ISL(inter switch link): Đây là khung đóng gói trunking theo chuẩn của các thiết bị cisco.

## Cấu hình Trunking

Chọn chuẩn 802.1q hay ISL(Các dòng Sw 2900 mặc định là dot1q và không hỗ trợ ISL, 3500 trở lên là cần vì nó hỗ trợ cả 2 chuẩn)

`` Switch(config-if)#switchport trunk encapsulation [dot1q|ISL] ``

Chuyển mode trunk và các mode khác:

``Switch(config-if)#switchport mode [access|trunk|desiable|auto]``

> Trong đó: 
- mode access: Cổng hỗ trợ truy cập dữ liệu (non-trunking).
- mode trunk: Cổng hỗ trợ trunking.
- mode desiable: Đặt interface tương ứng ở trạng thái "thử" chuyển the link sang trunk link. Interface khi đuợc cấu hình thế này sẽ chuyển sang mode trunk nếu interface láng giềng được set thành trunk, desirable, hay auto mode. Nếu interface láng giềng được set thành access hay non-negotiate thì "the link" sẽ trở thành non-trunking link.
- mode auto: Đặt interface sẵn sàng trở thành để chuyển từ 'the link' sang trunk link nếu interface láng giềng được set là trunk, hay desirable mode. 

Để kiểm tra bảng VLAN

``Switch#show vlan``

Nếu port nào đã lên trunk hoặc đã chết thì nó sẽ không thuộc VLAN nào cả.

Kiểm tra port trunk: 

``Switch#show interface trunk``

# VTP (VLAN Trunking Protocol)

## VTP là gì ?

**VTP** hay **VLAN Trunking Protocol** là giao thức độc quyền của Cisco hoạt động ở lớp 2. Giao thức này giúp tự động đồng bộ cấu hình VLAN bằng cách thêm, sửa, xóa thông tin về VLAN trong một hệ thống mạng. Việc cài đặt VTP giúp giải quyết một số vấn đề nằm bên trong môi trường mạng LAN như việc cấu hình VLAN không đúng gây chồng chéo các kết nối, hay cấu hình không đúng giữa các môi trường truyền khác nhau.

VTP có ba sự lựa chọn chế độ làm việc cho Switch: Server, Client và Transparent. Tùy thuộc vào mục đích quản trị và hạ tầng mạng mà ta lựa chọn sao cho hợp lý. Bảng sau đây tóm tắt sự khác nhau giữa ba chế độ làm việc:

![image](https://user-images.githubusercontent.com/79156398/163939526-be375d4a-29dd-4b52-be85-6f70d9a22416.png)

- Chế độ Server

	- Gửi hoặc chuyển tiếp thông tin quảng bá
	- Đồng bộ hóa thông tin VLAN
	- Lưu cấu hình vào NVRAM

- Chế độ Client

	- Chuyển tiếp thông tin quảng bá
	- Đồng bộ hóa thông tin VLAN
	- Không lưu cấu hình vào NVRAM

- Chế độ Transparent

	- Có thể tạo, chính sửa và xóa VLAN
	- Chuyển tiếp thông tin quảng bá
	- Không đồng bộ hóa thông tin VLAN
	- Lưu cấu hình vào NVRAM

