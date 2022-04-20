# Các giao thức định tuyến

Mạng lưới internet gồm vô vàn các thiết bị trải khắp mọi nơi trên thế giới. Để chúng có thể giao tiếp được với nhau, các thiết bị định tuyến đóng một vai trò hết sức quan trọng. Ở trên mạng lưới internet, chúng giống như những người điều hướng giao thông đứng giữa các ngã 3, ngã tư miệt mài phân luồng, điều hướng các phương tiện giao thông lúc giờ tan tầm. Nhưng không giống như các phương tiện giao thông, dữ liệu của chúng ta không thể tự mình đi tới điểm đích được mà cần được chỉ đường. Các switch, router, .. lúc này sẽ làm công việc định tuyến đường. Định tuyến có 2 kiểu: Định tuyến động và định tuyến tĩnh. Ở định tuyến tĩnh, chúng ta sẽ phải cấu hình các đường đi sẵn cho gói tin. Nếu gói tin không khớp các đường đi thì nó sẽ bị drop. Ở định tuyến động, các thiết bị định tuyến thông minh hơn, chúng có thể tự học các tuyến đường thông qua nhau, nhưng mất thêm một chút thời gian do phải học. Khi có tuyến đường chúng truyền tay nhau các gói tin lần lượt để gói tin đó có thể đến được router đích, nơi chứa máy tính cần nhận tin. Và để biết phải truyền tay cho ai thì các thiết bị định tuyến sử dụng các giao thức định tuyến. Các giao thức định tuyến có nhiều cách phân loại.

- Phân loại theo phạm vi hoạt động: Theo khu vực hoạt động thì có định tuyến trong (IGP - Interior Gateway Protocol) và định tuyến ngoài (EGP - Exterior Gateway Protocol). 
	- Định tuyến trong là loại giao thức chạy giữa các router nằm bên trong AS - Anonymous System ( vùng tự trị ).  Các AS thường là các ISP. Tiêu biểu như giao thức RIP, OSPF, EIGRP. 
	- Định tuyến ngoài là loại giao thức được dùng để chạy giữa các Router thuộc AS khác nhau. Tiêu biểu là giao thức BGP (Border Gateway Protocol).

- Phân loại theo cách các thiết bị giao tiếp: có Distance-vector, Link-state và Hybrid.
	- Distance-vector: là loại định tuyến mà mỗi router sẽ gửi cho láng giềng bảng định tuyến của nó theo định kỳ. Tiêu biểu chính là giao thức RIP.Đặc thù của loại hình định tuyến này là có khả năng bị loop nên cần 1 bộ quy tắc chống loop có thể sẽ làm chậm tốc độ hội tụ của giao thức.
	- Link-state: Mỗi Route sẽ gửi các bản tin trạng thái đường link LSA cho các Router khác . Việc tính toán định tuyến được thực hiện bằng giải thuật Dijkstra . 
	- Hybrid: Kết hợp đặc điểm của 2 loại trên. Tiêu biểu là EIGRP.

- Phân loại theo cấu trúc bảng định tuyến: Classful và classless
	- Classful: Router sẽ không gửi kèm theo subnet-mask trong bảng định tuyến của mình.
 	- Classless: Router sẽ gửi kèm theo subnet-mask trong bảng định tuyến của mình.

## Metric, giá trị AD 

Các giao thức định tuyến khi xây dựng bảng định tuyến sẽ có một giá trị là metric. Giá trị này xác định tuyến đường nào sẽ được ưu tiên gửi gói tin đi hơn. Mỗi loại giao thức lại có một cách tính metric khác nhau:

- RIP : tính metric bằng hop count.

- OSPF : tính metric bằng cost (10^8/bandwidth)

- EIGRP : Tính metric bằng cost dựa trên bandwidth, delay, load, reliability, MTU.

Trong trường hợp trên đường truyền có nhiều giao thức khác nhau thì sao ? Lúc này, các giá trị metric không đồng bộ nên không sử dụng được nữa. Vậy nên, để có thể chọn quãng đường đi, người ta sử dụng thêm giá trị là **AD - Administrative Distance**, giao thức nào có AD nhỏ hơn sẽ được ưu tiên hơn. Bảng giá trị AD được đề cập như sau: 


Sở dĩ có sự ưu tiên này một phần là dựa trên tốc độ hội tụ của các giao thức. Tốc độ hội tụ là khoảng thời gian để các router trong mạng học được hết các bảng định tuyến của nhau. Ở chế độ cấu hình tĩnh, mạng không hội tụ với mọi thay đổi diễn ra trên mạng ngoại trừ các chuyển đổi trạng thái up/down của ác cổng chính Router được cấu hình static route. Các giao thức định tuyến động thì thời gian hội tụ được sắp xếp giảm dần từ RIP (hội tụ chậm), OSPF (hội tụ nhanh), EIGRP (hội tụ rất nhanh ).

## RIP
*Sẽ cập nhật sau*
## OSPF
*Sẽ cập nhật sau*
## EIGRP
*Sẽ cập nhật sau*
## BGP
*Sẽ cập nhật sau*
## Định tuyến tĩnh
*Sẽ cập nhật sau*
