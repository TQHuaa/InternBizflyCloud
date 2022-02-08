## Biến môi trường là gì?
Biến môi trường trong Linux là các giá trị có thể thay đổi với mục đích sử dụng cho hệ thống như: Username, default home directory của user, đường dẫn đến các ứng dụng,... Biến môi trường có thể chỉnh sửa được từ người dùng.

## Cách sử dụng biến môi trường trong Linux

Để xem tất cả biến môi trường trong Ubuntu, dụng lệnh ``env`` hoặc ``printenv``

<img src="https://github.com/TQHuaa/TrainningVCCloud/blob/main/Pics/1e6e79356d45a11bf854.jpg">

Để xem các biến cụ thể, sử dụng ``printenv <tên biến>``

``printenv HOME``

Để thay đổi biến môi trường, sử dụng lệnh ``export``

``export HOME=/home/ubuntu``

Để xóa biến, sử dụng ``unset <tên biến>``

``unset HOME``

## Tài liệu tham khảo
https://www.hostinger.vn/huong-dan/linux-environment-variable
LPIC-1
