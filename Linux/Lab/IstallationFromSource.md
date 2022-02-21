# Cài đặt Nginx từ source

NGINX là một web server mạnh mẽ mã nguồn mở. Nginx sử dụng kiến trúc đơn luồng, hướng sự kiện vì thế nó hiệu quả hơn Apache server. Nó cũng có thể làm những thứ quan trọng khác, chẳng hạn như load balancing, HTTP caching, hay sử dụng như một reverse proxy. Trong nhiều trường hợp, ta sẽ cần phải modify nginx để phù hợp với một số nhu cầu riêng. Bài viết này sẽ hướng dãn cài đặt Nginx từ trên mã nguồn của nhà phát triển.

## Chuẩn bị sẵn sàng cho máy chủ

Trước tiên, ta cần đảm bảo rằng các gói của bạn được cập nhật:

``apt-get update -y``

![image](https://user-images.githubusercontent.com/79156398/154918835-b0f58fe9-99a7-49c9-85a3-b87175bea325.png)

Tiếp theo, bạn cần đảm bảo rằng bạn có sẵn một trình biên dịch. Chạy lệnh này để cài đặt build-essential:

``apt-get install build-essential -y``

![image](https://user-images.githubusercontent.com/79156398/154919025-2662d5d0-5154-4f58-96a6-e5ce2482277f.png)

## Tải xuống và cài đặt các phụ thuộc

Ta có thể sử dụng apt-get để xử lý:

``sudo apt-get install build-essential libpcre3 libpcre3-dev zlib1g zlib1g-dev libssl-dev libgd-dev libxml2 libxml2-dev uuid-dev -y``

![image](https://user-images.githubusercontent.com/79156398/154923316-72f867c7-726b-47c0-a109-20f77fba83ae.png)

## Tải xuống gói nguồn

Trước tiên, ta cần lên trang cung cấp mã nguồn(Trang chủ, Git,..) để tải bản nén của mã nguồn.

![image](https://user-images.githubusercontent.com/79156398/154924022-ff1eaf0d-3cba-414b-afbc-8f84010fec70.png)

Dùng lệnh wget để tải gói source từ trang chủ về.

``wget http://nginx.org/download/nginx-1.20.0.tar.gz``

![image](https://user-images.githubusercontent.com/79156398/154923858-5bd16883-87c7-4e62-bd7d-fdd068ffc5e9.png)

Tiếp theo, chúng ta cần giải nén kho lưu trữ và cd (thay đổi thư mục) vào thư mục git mới:

````
tar -xvzf nginx-1.20.0.tar.gz 
cd nginx-1.20.0/
```` 

Bây giờ, hãy xác minh rằng tất cả các phụ thuộc cần thiết để xây dựng gói đều có sẵn bằng cách chạy lệnh này:

``./configure --prefix=/usr``

Kết quả 

![image](https://user-images.githubusercontent.com/79156398/154924972-ec86b21d-c758-4326-b879-b14554906c37.png)

## Xây dựng

Có nhiều tùy chọn cấu hình có sẵn trong NGINX, bạn có thể sử dụng tùy theo nhu cầu của mình. Có nhiều mô-đun đi kèm với NGINX được cài đặt sẵn Nếu bạn không cần một mô-đun được xây dựng theo mặc định, bạn có thể tắt nó bằng cách đặt tên cho nó bằng --without-<MODULE-NAME>tùy chọn trên tập lệnh cấu hình, ví dụ:

``./configure --without-http_empty_gif_module``  
  
Sau khi hoàn tất cấu hình tùy chỉnh, bây giờ chúng ta có thể biên dịch mã nguồn NGINX bằng cách sử dụng lệnh sau:

``make``

![image](https://user-images.githubusercontent.com/79156398/154927891-f38aee24-0961-4a74-8f17-1d5ead5769fa.png)

Bây giờ tất cả các tệp nhị phân đã được xây dựng, đã đến lúc cài đặt nginx:

``make install``

Kết quả 
  
![image](https://user-images.githubusercontent.com/79156398/154927999-78204d64-aaa9-4d4f-ab11-c213aac080c9.png)
  
Done! Ta khởi động nginx bằng lệnh này : ``nginx``  

Điều cuối cùng cần làm là xác minh rằng git đang hoạt động:

``nginx -V``

Đầu ra sẽ giống như sau:

![image](https://user-images.githubusercontent.com/79156398/154928880-4b523668-3928-40fd-b9de-a68649ed7a5a.png)

Phiên bản ngắn gọn của các lệnh trên :

````
wget link [output]
tar -xvzf file.tar.gz
cd into folder
./configure --prefix=/usr && make && make install
````

## Tham khảo
  
https://www.alibabacloud.com/blog/how-to-build-nginx-from-source-on-ubuntu-20-04-lts_597793
