![image](https://user-images.githubusercontent.com/79156398/156970710-78b528c1-da8a-4298-94b6-d3a0c8376247.png)

![image](https://user-images.githubusercontent.com/79156398/156970740-7ced8017-44b5-428c-bb33-b339ba331cfc.png)

![image](https://user-images.githubusercontent.com/79156398/156970813-5420c2e6-31fc-47f4-b443-20879d451e85.png)

![image](https://user-images.githubusercontent.com/79156398/156970854-f5977d51-c34b-4f02-95df-23e7adbf9eb1.png)

![image](https://user-images.githubusercontent.com/79156398/156970877-fad7d6d9-d208-4e95-9465-f49879080928.png)

![image](https://user-images.githubusercontent.com/79156398/156970908-4ac3f31b-7085-4a2d-b313-7141b776def7.png)

![image](https://user-images.githubusercontent.com/79156398/156989496-97b0a74a-7f9d-4ae4-ace3-b8a9ba92dacc.png)

![image](https://user-images.githubusercontent.com/79156398/156987931-6f22f28b-02be-4940-974f-72181d1f8e06.png)

# Cấu hình RSnapshot
## Chuẩn bị
Cấu hình ssh để 
File cần đồng bộ là file .ssh

## Cấu hình
Đầu tiên, ta cần tải rsync và rsnapshot về máy tính.

``apt-get isntall -y rsync rsnapshot``

Tiếp theo, ta tiến hành cấu hình rsnapshot bằng cách truy cập đường dẫn ``/etc/rsnapshot.conf``:

``vi /etc/rsnapshot.conf``

Các tùy chọn trong file này đã khá chi tiết, một số tùy chọn chính sẽ được bài viết này sử dụng. Cấu trúc của file gồm các phần chính như sau: 

- CONFIG FILE VERSION : Vì là mã nguồn mở, file config của rsnapshot có thể được cập nhật nên có 1 trường chứa thông tin về phiên bản của file config.

- SNAPSHOT ROOT DIRECTORY : Chứa thông tin về thư mục đích sẽ lưu trữ bản sao.
- EXTERNAL PROGRAM DEPENDENCIES : Link tới các ứng dụng cần thiết cho quá trình đồng bộ.
- BACKUP LEVELS/INTERVALS : Cấu hình tự động sao lưu và quản lý các bản sao lưu.
- GLOBAL OPTIONS : Chứa các cài đặt bổ sung.
- BACKUP POINTS / SCRIPTS :  Nơi chỉ định file, thư mục được sao lưu.

Tại file ``rsnapshot.conf``, sửa đổi phần snapshot_root để chỉ ra nơi chúng ta sẽ lưu trữ các bản sao lưu trên máy tính từ xa:
| *snapshot_root /usr/backup*
Tại phần *EXTERNAL PROGRAM DEPENDENCIES*, thêm các chương trình cần thiết bằng cách uncomment dòng tương ứng. Như ở hình dưới đây, tôi đã sử dụng ``cp`` để copy, ``rm`` để xóa,  ``rsync`` và ``ssh`` để đồng bộ sang máy chủ khác,  ``logger`` để ghi nhật ký.
Phần *BACKUP LEVELS/INTERVALS*, uncomment các tùy chọn ``retain`` và thêm các chỉ dẫn về thời gian để đồng bộ. Trong trường hợp của mình, tôi thêm các chỉ dẫn để đồng bộ fie





## Tham khảo




