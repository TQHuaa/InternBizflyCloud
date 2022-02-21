1. Chuẩn bị sẵn sàng cho máy chủ

Trước tiên, ta cần đảm bảo rằng các gói của bạn được cập nhật:

``apt-get update -y``
![image](https://user-images.githubusercontent.com/79156398/154907789-4cd2b574-6860-4201-9b5b-e9b7fe8e6b7f.png)

Tiếp theo, bạn cần đảm bảo rằng bạn có sẵn một trình biên dịch. Chạy lệnh này để cài đặt build-essential:

``apt-get install build-essential -y``

2. Tải xuống và cài đặt các phụ thuộc

Ta có thể sử dụng apt-get để xử lý:

``apt install build-essential dh-autoreconf libcurl4-gnutls-dev libexpat1-dev gettext libz-dev libssl-dev -y``

![image](https://user-images.githubusercontent.com/79156398/154909444-11a0e5b5-1c1c-4419-9606-6a689c2bdd31.png)

3. Tải xuống gói nguồn

``wget https://github.com/git/git/archive/refs/tags/v2.35.1.tar.gz``

![image](https://user-images.githubusercontent.com/79156398/154909814-893e2fab-9602-4c7c-b616-86ce9a403f9a.png)

Tiếp theo, chúng ta cần giải nén kho lưu trữ và cd (thay đổi thư mục) vào thư mục git mới:

````
tar -xvzf v2.23.0.tar.gz
cd git-2.23.0/
````
![image](https://user-images.githubusercontent.com/79156398/154911576-3638ea5d-cfcd-421a-a9fa-84bbf19de6cf.png)

7. Cài đặt Git

Bây giờ chúng ta đã giải nén gói của mình và sẵn sàng sử dụng, chúng ta cần cấu hình nó:

``make configure``

Ta sẽ thấy một đầu ra tương tự như sau:

````
GIT_VERSION = 2.23.0
GEN configure
````

Tiếp theo, hãy xác minh rằng tất cả các phụ thuộc cần thiết để xây dựng gói đều có sẵn bằng cách chạy lệnh này:

``./configure --prefix=/usr``

Kết quả 
![image](https://user-images.githubusercontent.com/79156398/154914912-b8b145f3-a53a-4857-8e8b-c6c468422805.png)

Sau đó, chúng ta sẽ xây dựng mã nguồn:

``make all``
![image](https://user-images.githubusercontent.com/79156398/154917100-ce808a4e-a7b8-4d63-85e7-2601febbee3f.png)

Bây giờ tất cả các tệp nhị phân đã được xây dựng, đã đến lúc cài đặt git:

``make install``
![image](https://user-images.githubusercontent.com/79156398/154917549-f27cae3f-9369-408c-abef-8452c70e94d5.png)

Điều cuối cùng cần làm là xác minh rằng git đang hoạt động:

``git --version``

Đầu ra sẽ giống như sau:

![image](https://user-images.githubusercontent.com/79156398/154917597-ff5d59f9-12ea-4fba-b142-05cac2310041.png)

Phiên bản ngắn gọn của các lệnh trên :

````
wget file
tar -xvzf file
cd into folder
./configure && make && make install
````
