# HTTP

## HTTP là gì ? 

**HTTP** là viết tắt của **HyperText Transfer Protocol** - giao thức truyền tải siêu văn bản được sử dụng trong WWW (**World Wide Web**). Là một giao thức liên quan đến web server nên được sử dụng thường xuyên nhất trong bộ các giao thức thuộc TCP/IP.

HTTP hoạt động dựa trên mô hình Client-Server (mô hình khách chủ). Các máy tính của người dùng sẽ đóng vai trò làm máy khách và yêu cầu các nội dung bên phía server, phía server phản hồi lại và trả về dữ liệu hoặc không. Hoạt động trên cổng TCP/80, header của HTTP được cho như hình dưới.


## Các phiên bản 

Phiên bản hoàn chỉnh đầu tiên của HTTP là HTTP 0.9 (Ra đời năm 1991), Tiếp theo là HTTP 1.0 (Giới thiệu chính thức năm 1996), HTTP 1.1 (1997) và mới đây nhất là HTTP 2.0. Các phiên bản sau ra đời nhằm thay thế phiên bản trước, kế thừa những chức năng cốt lõi của phiên bản trước nhưng có nhiều cải tiến và bổ sung. Hiện nay thì HTTP 2.0 chưa được dùng phổ biến do còn khá mới và do các doanh nghiệp Web cũng phần nào ngại chuyển đổi. Do vậy, HTTP 1.1 vẫn là giao thức HTTP phổ biến nhất. HTTP 1.0 vẫn còn được sử dụng nhiều trong hệ thống Proxy và một số ứng dụng cũ (wget). 
==(Để tìm hiểu vì sao HTTP 1.0 vẫn còn được dùng nhiều trong các hệ thống Proxy thì ta phải nắm HTTP 1.0 và HTTP 1.1 cache dữ liệu như thế nào?)==

## Cách hoạt động của HTTP 

![image](https://user-images.githubusercontent.com/79156398/164357021-5f93d53e-d95b-4768-96d0-8e56831b078d.png)

Thông thường mỗi HTTP Request sẽ sử dụng một kết nối TCP (TCP Connection). Các bước sẽ trải qua đại khái như sau:
1. Phía client sẽ khởi tạo một kết nối TCP đến server.
2. Sau khi kết nối thành công, client sẽ gởi request đến server.
3. Server tiếp nhận request, tiến hành tìm kiếm và trả về cho client thông qua kết nối TCP ở bước 2.
4. Client tiếp nhận response từ server.
5. Client đóng kết nối TCP.
6. Nếu client cần thêm các object từ server, mỗi object sẽ cần thực hiện lại các bước 1 đến 5.

Ở đây chúng ta cần lưu ý rằng, bản chất TCP Connection khi được thiết lập sẽ cần 3 bước được biết đến với tên gọi: TCP 3-Way Handshake Process. Tức là giữa client và server cần trao đổi (gởi và nhận) 3 messages trước khi kết nối được thiết lập. Tương tự khi kết nối đóng lại cũng cần thực hiện lại quy trình 3 bước này. Việc phải thực hiện đi thực hiện lại quy trình kết nối 3 bước là một điểm yếu rất lớn của HTTP 0.9 và 1.0. Đây là một trong những lý do thúc đẩy sự phát triển lên HTTP 1.1.

## Header Request HTTP
Mỗi khi muốn lấy dữ liệu, một HTTP client (máy khách) gửi một HTTP request (yêu cầu) lên server (máy chủ) nhờ một thông điệp có định dạng như sau:
````
<method> <request-URL> <http-serverion>
<headers>
<body>
````
ví dụ: 

![image](https://user-images.githubusercontent.com/79156398/164360600-0de8e927-d6c2-408d-9571-19e3fd65bd85.png)

### 1. Request Line
Dòng đầu của HTTP Request sẽ là Request Line gồm 3 thành phần: 
- Method : phương thức sử dụng 
- Request URL/URI: Xác định tài nguyên web
- HTTP Version: Phiên bản HTTP sử dụng

![image](https://user-images.githubusercontent.com/79156398/164359463-8824ebcc-926a-447a-b536-d82fa26a3cf0.png)

### 2. Request Header
Tiếp theo dòng Request-Line là các trường Request-header, cho phép client gửi thêm các thông tin bổ sung về thông điệp HTTP request và về chính client. Một số trường thông dụng như:
- Accept loại nội dung có thể nhận được từ thông điệp response. Ví dụ: text/plain, text/html…
- Accept-Encoding: các kiểu nén được chấp nhận. Ví dụ: gzip, deflate, xz, exi…
- Connection: tùy chọn điều khiển cho kết nối hiện thời. Ví dụ: keepalive,Upgrade…
- Cookie: thông tin HTTP Cookie từ server
- User-Agent: thông tin về user agent của người dùng.

![image](https://user-images.githubusercontent.com/79156398/164362734-1eb754a0-d36a-4251-b4de-3bbc28bcc08d.png)

### 3. Request Body 
Body là dữ liệu mà Client sẽ gửi lên Server.

## Header Response HTTP
HTTP response là bản tin trả về từ server sang client, trong đó sẽ có các trường thông tin mà request yêu câu.

Định dạng gói tin HTTP response cũng gồm 3 phần chính là: Status line, Header và Body.

![image](https://user-images.githubusercontent.com/79156398/164361270-5dc0cadd-70ca-4199-9f76-ba487400f4b1.png)

### Response Status Line
Gồm 3 trường là phiên bản giao thức (HTTP version), mã trạng thái (Status code) và mô tả  trạng thái (Status text):
- Phiên bản giao thức (HTTP version): phiên bản của giao thức HTTP mà server hỗ trợ, thường là HTTP/1.0 hoặc HTTP/1.1
- Mã trạng thái (Status code): mô tả trạng thái kết nối dưới dạng số, mỗi trạng thái sẽ được biểu thị bởi một số nguyên. Ví dụ: 200, 404, 302,…
- Mô tả trạng thái (Status text): mô tả trạng thái kết nối dưới dạng văn bản một cách ngắn gọn, giúp người dùng dễ hiểu hơn so với mã trạng thái. Ví du: 200 OK, 404 Not Found, 403 Forbiden,…

![image](https://user-images.githubusercontent.com/79156398/164361594-79835c97-1d8c-487c-8cff-9b6af1166fc9.png)

### Response Header
Header của gói tin response có chức năng tương tựn như gói tin request, giúp server có thể truyền thêm các thông tin bổ sung đến client dưới dạng các cặp “Name:Value”.

### Response Body
Là nơi đóng gói dữ liệu để trả về cho client, thông thường trong duyệt web thì dữ liệu trả về sẽ ở dưới dạng một trang HTML để trình duyệt có thể thông dịch được và hiển thị ra cho người dùng.

Hoặc trả về dạng JSON, XML khi giao tiếp bằng API.

## Các phương thức HTTP
Request Method phổ dụng của HTTP:
- GET
- HEAD
- POST
- PUT
- DELETE
- TRACE
- OPTIONS
- CONNECT
- PATCH

### Phương thức GET

Câu truy vấn sẽ được đính kèm vào đường dẫn HTTP request. Ví dụ: /?username=”tinohost”&pass=”tenmien”
GET request có thể được cached, bookmark và lưu trong lịch sử của trình duyệt mà bị giới hạn về chiều dài (chiều dài của URL là có hạn).
Lưu ý: Bạn không nên dùng GET request với dữ liệu quan trọng mà chỉ dùng để nhận dữ liệu, không có tính bảo mật.

### Phương thức POST

Câu truy vấn sẽ được gửi trong phần message body của HTTP request.
POST không thể, cached, bookmark hay lưu trong lịch sử trình duyệt và cũng không bị giới hạn về độ dài.

###Các phương thức khác

HEAD: tương tự như GET nhưng chỉ gửi về HTTP header.
PUT: tải lên một mô tả về URL định trước.
DELETE: xóa một tài nguyên định trước.
OPTIONS: trả về phương thức HTTP mà server hỗ trợ.
CONNECT: chuyển kết nối của HTTP request thành một kết nối HTTP tunnel.

## Response Status thông dụng
Một số loại thông dụng mà server trả về cho client như sau:

**1xx: information Message**
Các status code này chỉ có tính chất tạm thời, client có thể không quan tâm.

**2xx Successful**
Khi đã xử lý thành công request của client, server trả về status dạng này:

- 200 OK: request thành công.
- 202 Accepted: request đã được nhận, nhưng không có kết quả nào trả về, thông báo cho client tiếp tục chờ đợi.
- 204 No Content: request đã được xử lý nhưng không có thành phần nào được trả về.
- 205 Reset: giống như 204 nhưng mã này còn yêu câu client reset lại document view.
- 206 Partial Content: server chỉ gửi về một phần dữ liệu, phụ thuộc vào giá trị range header của client đã gửi.

**3xx Redirection**
Server thông báo cho client phải thực hiện thêm thao tác để hoàn tất request:

- 301 Moved Permanently: tài nguyên đã được chuyển hoàn toàn tới địa chỉ Location trong HTTP response.
- 303 See other: tài nguyên đã được chuyển tạm thời tới địa chỉ Location trong HTTP response.
- 304 Not Modified: tài nguyên không thay đổi từ lần cuối client request, nên client có thể sử dụng đã lưu trong cache.

**4xx Client error**
Lỗi của client:

- 400 Bad Request: request không đúng dạng, cú pháp.
- 401 Unauthorized: client chưa xác thực.
- 403 Forbidden: client không có quyền truy cập.
- 404 Not Found: không tìm thấy tài nguyên.
- 405 Method Not Allowed: phương thức không được server hỗ trợ.

**5xx Server Error**
Lỗi của server:

- 500 Internal Server Error: có lỗi trong quá trình xử lý của server.
- 501 Not Implemented: server không hỗ trợ chức năng client yêu cầu.
- 503 Service Unavailable: Server bị quá tải, hoặc bị lỗi xử lý.

![image](https://user-images.githubusercontent.com/79156398/164362133-b549ee8d-c287-4e46-ad1d-e07dc78a4a2f.png)

## Điểm mạnh của HTTP
- Đơn giản.
- Cho phép giảm lưu lượng mạng vì ít kết nối TCP hơn.
- Giảm mức sử dụng bộ nhớ do ít dữ liệu kết nối đồng thời. 

## Điểm yếu của HTTP 
- Chưa được bảo mật.
