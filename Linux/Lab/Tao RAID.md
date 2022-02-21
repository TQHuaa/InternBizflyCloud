# Tạo RAID bằng mdadm

## RAID quick start

RAID là hình thức ghép nhiều ổ đĩa lại với mục đích tăng dung lượng hoặc tăng tính an toàn cho dữ liệu, hoặc kết hợp cả hai. 

Một số note để hiểu qua về RAID: 
- RAID có thể dùng cho bất kỳ hệ điều hành nào, từ Window 98, window 2000, window XP, Window 10, window server 2016, MAC OS X, Linux…vv
- RAID chỉ hoạt động trên các ổ đĩa có dung lượng bằng nhau. 
- RAID 0 có tác dụng gộp các ổ đĩa lại để lưu trữ chung. 
- RAID 1 dùng 1 ổ để lưu + 1 ổ sao lưu dự phòng, số ổ phải là 2n.
- RAID 10 kết hợp giữa RAID 1 và RAID 0.
- RAID 5 dung lượng khi kết hợp lại sẽ ít hơn 1 ổ đĩa.
- RAID 6 dung lượng khi kết hợp lại sẽ ít hơn 2 ổ đĩa.

![image](https://user-images.githubusercontent.com/79156398/154930484-a1476cdd-e02c-44e9-bfa4-deeb460eb401.png)

Giờ ta đã hiểu sơ qua về RAID, thử tạo thôi! 

## Chuẩn bị

Để tạo RAID cần rất nhiều ổ cứng. RAID 0, RAID 1 cần tối thiểu 2 disks, RAID 5 cần 3 disks, RAID 6, RAID 10 cần 4 disks tối thiểu [2]. Vì thế cài đặt máy ảo trên VMWare để lab là phương pháp tối ưu và tiết kiệm chi phí nhất. Để cài đặt VM, ta có thể xem tại [đây](https://github.com/TQHuaa/TrainingVCCloud/blob/main/Linux/T%E1%BB%95ng%20Quan/C%C3%A1c%20c%C3%B4ng%20c%E1%BB%A5%20%E1%BA%A3o%20h%C3%B3a.md).

### Thêm disk vào VM 

Để attach ổ đĩa, máy ảo cần phải được tắt. Ở đây ta ví dụ bằng VM Ubuntu Server 20.04: 

![image](https://user-images.githubusercontent.com/79156398/154933155-664ee879-411f-45f0-a141-9e71b82d9826.png)

Chuột phải vào máy ảo, chọn Setting, cửa sổ Virtual Machine Settings sẽ hiện ra. 

![image](https://user-images.githubusercontent.com/79156398/154933459-ecfb86f0-56f1-4b34-93a6-4189c7a5e795.png)

Chọn Add > Hard Disk > next.

![image](https://user-images.githubusercontent.com/79156398/154933659-2b281b47-cf69-4f28-b9a1-b87e0321130d.png)

Chọn SCSI > next. 

![image](https://user-images.githubusercontent.com/79156398/154933806-1ea51359-3813-4335-8978-f863bc06cade.png)

Tạo ổ đĩa ảo mới

![image](https://user-images.githubusercontent.com/79156398/154933879-feef77d1-4c73-43df-8984-de8f2f6e9e6a.png)

Tiếp theo ta tùy chọn cấu hình size ổ đĩa. Ngoài ra, ta có 2 lựa chọn là *Store virtual disk as Single file* - lưu dữ liệu ổ đĩa ảo vào 1 file *.vmdk duy nhất và *Split virtual disk into multiple file* - lưu ra nhiều file *.vmdk

![image](https://user-images.githubusercontent.com/79156398/154934256-0449c012-18d6-410b-b975-98f9ba63f221.png)

Cuối cùng đặt tên và Finish.

Lặp lại vài lần các bước trên .Vậy là hoàn tất việc attach ổ cứng để tạo môi trường lab.

### Tải mdadm

Sau khi chuẩn bị phần cứng ảo, ta cần khởi chạy VM, cập nhật hệ thống và tải mdadm về. 

![image](https://user-images.githubusercontent.com/79156398/154935574-577e9e06-b9b3-4a3b-b79a-ce14bc1d87ea.png)

### Tạo phân vùng cho ổ đĩa

Để sử dụng ta cần tạo các phân vùng RAID trên các ổ đĩa. Kiểm tra danh sách các ổ đĩa , ta dùng ``fdisk -l | grep sd``

![image](https://user-images.githubusercontent.com/79156398/154936151-cd531aad-e76d-44c9-b135-515600f253a2.png)

Ở đây ta thấy sdg và sdf là hai ổ chưa có phân vùng. Ta thực hiện tạo phân vùng RAID cho chúng bằng fdisk 

``fdisk /dev/sdg``

![image](https://user-images.githubusercontent.com/79156398/154936593-8ece18d2-04e0-488e-8071-41902a260c95.png)

``m`` để getting help 

![image](https://user-images.githubusercontent.com/79156398/154936679-3413561b-e807-4b50-9681-0e97b091f6a0.png)

Tạo phân vùng mới, nhấn ``n``. Enter hết để tạo phân vùng primary với kích thước tối đa.

![image](https://user-images.githubusercontent.com/79156398/154936949-29223d21-c856-4c25-85d8-4010db91fb41.png)

Chọn ``t`` để thay đổi kiểu phân vùng. Nếu không rõ, ta có thể chọn ``l`` để xem toàn bộ các kiểu phân vùng. Trong trường hợp này, phân vùng RAID có mã hex là *fd*.

![image](https://user-images.githubusercontent.com/79156398/154937558-ed635758-b6b7-425c-b06d-5d14116ef87f.png)

Chọn ``w`` để lưu. Hoàn thành tạo phân vùng RAID.

## Tạo RAID 0

## Tạo RAID 1

## Tạo RAID 10

## Tạo RAID 5

## Tạo RAID 6

## Tham khảo 

https://blogd.net/linux/software-raid-toan-tap-tren-linux/#6-h%C6%B0%E1%BB%9Bng-d%E1%BA%ABn-t%E1%BA%A1o-raid

[2] - https://www.microsemi.com/product-directory/raid-controllers/4047-raid-levels#:~:text=RAID%206%20requires%20a%20minimum,drives%20in%20the%20RAID%20set.
