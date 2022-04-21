# ARP 
Mỗi máy tính thường có ít nhất một card mạng để có thể truy cập internet. Các card mạng có một địa chỉ MAC được cấp bởi nhà sản xuất và nó là duy nhất. Địa chỉ MAC này khá quan trọng. Với mô hình TCP/IP hay OSI, để gói tin có thể được đóng gói header ethernet. Máy tính cần phải biết địa chỉ MAC của máy nhận. Vấn đề đặt ra là làm sao để máy tính có thể biết được địa chỉ MAC của máy nhận. Đó là lý do chúng ta có giao thức ARP.

## Giao thức ARP là gì? 
Giao thức ARP là giao thức giúp chuyển đổi từ địa chỉ IP của thiết bị sang địa chỉ MAC. Đây là giao thức thuộc lớp 2 trong mô hình OSI. Header của ARP được cho ở hình dưới.

![image](https://user-images.githubusercontent.com/79156398/164196948-2786eb59-fa64-49ea-83a8-1dbef7dbf7ed.png)

Ý nghĩa của các gói tin trong header gói tin ARP là:

- Hardware Type: Xác định bộ giao tiếp phần cứng máy gửi cần biết. Có giá trị là 1 (0x0001) với đường truyền Ethernet.
- Protocol Type: Xác định kiểu giao thức máy gửi cung cấp. Có giá trị là 0x0800 cho giao thức IP
- HLEN (Hardware Address Length): Độ dài địa chỉ vật lý tính theo bit.
- PLEN (Protocol Address Length): Độ dài địa chỉ logic tính theo bit.
	- 1: ARP request.
	- 2: ARP reply.
	- 3: RARP request.
	- 4: RARP reply.
- Sender Hardware Address: Chứa địa chỉ MAC của máy gửi.
- Sender IP Address: Chứa địa chỉ IP của máy gửi.
- Target Hardware Address: Chứa địa chỉ MAC của máy nhận. Giá trị là 00:00:00:00:00:00 đối với gói tin Broadcast.
- Target IP Address: Chứ địa chỉ IP của máy nhận.

## Cơ chế hoạt động của ARP 

![image](https://user-images.githubusercontent.com/79156398/164198873-9f8e4df5-d7f0-48de-8292-720ae953e2ed.png)

Ví dụ với máy A là router hoặc host đang tìm kiếm máy có địa chỉ IP 192.168.1.220

1. Đầu tiên, router(Host) sẽ kiểm tra cache của mình. Nếu địa chỉ 192.168.1.220 không có trong cache, Router(Host) sẽ gửi gói tin ARP Request quảng bá tới tất cả các máy trong mạng hỏi xem địa chỉ IP 192.168.1.220 ở đâu.
2. Các máy nhận nếu không trùng với target IP sẽ tự động hủy gói. Nếu trùng IP target, nó sẽ khởi tạo 1 gói ARP Reply và gửi lại máy yêu cầu cùng lúc đó sẽ cập nhật địa chỉ IP và MAC vào bảng ARP cache để rút ngắn thời gian xử lý cho lần sau.
3. Router(Host) sau khi nhận ARP Reply cũng sẽ cập nhật vào bảng ARP Cache để sử dụng lần sau.

## Phân tích gói tin bằng wireshark

![image](https://user-images.githubusercontent.com/79156398/164200662-595d8d7f-74e0-49db-8944-292dec9a758d.png)
