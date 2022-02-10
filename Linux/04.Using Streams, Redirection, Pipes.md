# Streams trong Linux

## Khái niệm Streams 

Máy tính sử dụng luồng để truyền dữ liệu, trong Linux có 3 loại luồng dữ liệu cơ bản để truyền dữ liệu dạng văn bản là ``Standard Input (stdin)``, ``Standard Output (stdout)``, ``Standard Error (stderr)``.
Các luồng trong Linux — giống như hầu hết mọi thứ khác — được coi như thể chúng là tệp. Ta có thể đọc văn bản từ một tệp và bạn có thể ghi văn bản vào một tệp. Mỗi tệp được liên kết với một quy trình được cấp phát một số duy nhất để xác định nó. Đây được gọi là bộ mô tả tệp. Bất cứ khi nào một hành động được yêu cầu thực hiện trên tệp, bộ mô tả tệp được sử dụng để xác định tệp.
Những giá trị này luôn được sử dụng cho ``stdin``, ``stdout``, và ``stderr``:
  - 0: stdin
  - 1: stdout
  - 2: stderr
  
Trong Linux, **stdin** là dòng đầu vào tiêu chuẩn. Điều này chấp nhận văn bản làm đầu vào của nó. Đầu ra văn bản từ lệnh tới trình bao được gửi qua **stdout** (tiêu chuẩn ra) luồng. Thông báo lỗi từ lệnh được gửi qua **stderr** (lỗi tiêu chuẩn) luồng. 

## Redirection

Có thể thấy rằng có hai luồng đầu ra, stdout và stderr và một luồng đầu vào, stdin. Bởi vì các thông báo lỗi và đầu ra bình thường đều có ống dẫn riêng để đưa chúng đến cửa sổ đầu cuối, chúng có thể được xử lý độc lập với nhau. Ví dụ truyền output vào file out.txt và truyền lỗi vào file err.txt. Đây cũng chính là ví dụ về redirection.

- Redirect input: 
   ````
  ~$cat <<EOM >input.sh
  #!/bin/bash
  if [ -t 0 ]; then
    echo stdin coming from keyboard
  else
    echo stdin coming from a file
  fi
  EOM
  ````
  ````
  ~$./input.sh < a.txt
  stdin coming from a file 
  ```` // chuyển hướng từ stdint là bàn phím sang một tệp đầu vào
- Redirect output: ``echo "Hello" >> a.txt`` // chuyển hướng từ stdout là màn hình sang một tệp đầu ra 
- Redirect error: ``./error.sh 2> capture.txt`` // chuyển hướng lỗi sang tệp capture.txt bằng mô tả tệp cho stderr = 2
- Redirect output + error: ``./error.sh > capture.txt 2>&1`` // chuyển hướng lỗi + output sang tệp capture.txt

## Pipes

Đường ống (pipe) dùng để chuyển hướng trên hệ điều hành Linux, nó cho phép chúng ta sử dụng hai hoặc nhiều lệnh sao cho đầu ra của một lệnh đóng vai trò trực tiếp làm đầu vào của lệnh tiếp theo. Kết nối trực tiếp giữa các lệnh cho phép chúng hoạt động đồng thời và cho phép dữ liệu được truyền giữa chúng liên tục thay vì phải chuyển qua các tệp văn bản tạm thời hoặc qua màn hình hiển thị. Các đường ống là một chiều tức là luồng dữ liệu chuyển hướng từ trái sang phải qua đường ống.
Ví dụ: Nếu chạy lệnh ``env | grep HOME`` thay vì hiện hết các biến môi trường thì máy sẽ lọc các dòng có chuỗi *HOME*

## Tài liệu tham khảo 
https://khaidantri.net/stdin-stdout-va-stderr-tren-linux-la-gi
https://blogd.net/linux/duong-ong-loc-va-chuyen-huong-tren-linux/
LPIC-1
