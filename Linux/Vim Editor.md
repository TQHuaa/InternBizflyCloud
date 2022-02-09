## Lời dẫn

Các công cụ chỉnh sửa văn bản rất cần thiết khi sử dụng hệ điều hành Linux. Ta có thể sử dụng để tạo script, chỉnh sửa các file, ... Vì vậy, Linux cung cấp một vài công cụ chỉnh sửa văn bản rất hữu ích như: 
- emacs 
- nano 
- vim

Vim là một công cụ chỉnh sửa văn bản được cải tiến từ vi, là công cụ chỉnh sửa văn bản của Unix, vim là viết tắt của "vi improved". Để khởi chạy Vim, tại màn hình console, gõ `vi` hoặc `vim`.

## Các chế độ của Vim 

Vim Editor có 3 chế độ tiêu chuẩn : 
- **Command Mode** Hay còn gọi là **Normal Mode**, là giao diện đệm khi khởi chạy vim, chủ yếu để xem tài liệu dạng Read-Only hoặc làm chung gian chuyển đổi giữa các chế độ.
<img src="https://github.com/TQHuaa/TrainningVCCloud/blob/main/Pics/VimCommandMode.png">

*Normal Mode*

Để trở về chế độ Normal Mode, ta dùng tổ hợp ``Ctrl + C`` hoặc ``Esc``.
- **Insert Mode** Ở chế độ này, Vim soạn thảo giống như trình soạn thảo đơn thuần. 
<img src="https://github.com/TQHuaa/TrainningVCCloud/blob/main/Pics/VimInsertMode.png">

*Insert Mode

Các phím tắt vào chế độ Insert Mode (cần trở về chế độ Command Mode): 
````
 i - Đưa chế độ chèn vào vị trí con trỏ hiện tại.
 a - Đưa chế độ chèn sau vị trí hiện tại.
 I - Đưa chế độ chèn vào đầu dòng hiện tại.
 A - Đưa chế độ chèn vào cuối dòng hiện tại.
````

- **Ex Mode** được sử dụng để thao tác các câu lệnh bắt đầu bằng dấu ``:``.
<img src="https://github.com/TQHuaa/TrainningVCCloud/blob/main/Pics/VimExMode.png"> 

*Ex Mode*

Để vào chế độ Ex Mode, cần trở về chế độ Command Mode sau đó gõ ``:``. 
- Ngoài ra, Vim Editor còn có chế độ **Visual Mode**, sử dụng để bôi đen thao tác văn bản.
<img src="https://github.com/TQHuaa/TrainningVCCloud/blob/main/Pics/VimVisualMode.png">

*Visual mode*

Để vào chế độ Visual Mode, cần trở về chế độ Command Mode sau đó gõ ``v`` hoặc ``V``.

## Các câu lệnh thao tác trên Vim editor

### Ở chế độ Command Mode
| Lệnh  | Công dụng |
| ------------- | ------------- |
| h | Di chuyển con trỏ sang trái một ký tự. |
| l | Di chuyển con trỏ sang phải một ký tự. |
| j | Di chuyển con trỏ xuống một dòng (dòng tiếp theo trong văn bản). |
| k | Di chuyển con trỏ lên một dòng (dòng trước trong văn bản). |
| w | Di chuyển con trỏ về phía trước một từ trước từ tiếp theo. |
| đ | Di chuyển con trỏ đến cuối từ hiện tại. |
| b | Di chuyển con trỏ về phía sau một từ. |
| ^ | Di chuyển con trỏ đến đầu dòng. |
| $ | Di chuyển con trỏ đến cuối dòng. |
| gg | Di chuyển con trỏ đến dòng đầu tiên của tệp. |
| G | Di chuyển con trỏ đến dòng cuối cùng của tệp. |
| nG | Di chuyển con trỏ đến dòng n. |
| ZZ | Ghi bộ đệm vào tệp và thoát khỏi trình chỉnh sửa. |
| Ctrl + B | Cuộn lên toàn màn hình. |
| Ctrl + F | Cuộn xuống toàn màn hình. |
| Ctrl + U | Cuộn lên nửa màn hình. |
| Ctrl + D | Cuộn xuống một nửa màn hình. |
| Ctrl + Y | Cuộn lên một dòng. |
| Ctrl + E | Cuộn xuống một dòng. |


### Ở chế độ Insert Mode
| Lệnh  | Công dụng |
| ------------- | ------------- |
| a | Chèn văn bản sau con trỏ. |
| A | Chèn văn bản vào cuối dòng văn bản. |
| dd | Xóa dòng hiện tại. |
| dw | Xóa từ hiện tại. |
| i | Chèn văn bản trước con trỏ. |
| I | Chèn văn bản trước khi bắt đầu dòng văn bản. |
| o | Mở một dòng văn bản mới bên dưới con trỏ và chuyển sang chế độ chèn. |
| O | Mở một dòng văn bản mới phía trên con trỏ và chuyển sang chế độ chèn. |
| p | Dán văn bản đã sao chép vào sau con trỏ. |
| P | Dán văn bản đã sao chép trước con trỏ. |
| yw | Sao chép từ hiện tại. |
| yy | Sao chép dòng hiện tại. |


### Ở chế độ Ex Mode
| Lệnh  | Công dụng |
| ------------- | ------------- |
| :! *command* | Thực thi shell *command* và hiển thị kết quả, nhưng không thoát khỏi trình chỉnh sửa. |
| : r! *command* | Thực hiện shell *command* và đưa kết quả vào vùng đệm của trình soạn thảo. |
| : r *file* |  Đọc nội dung *file* và đưa chúng vào vùng đệm của trình soạn thảo. |
| : x | Ghi bộ đệm vào tệp và thoát khỏi trình chỉnh sửa. |
| : wq | Ghi bộ đệm vào tệp và thoát khỏi trình chỉnh sửa. |
| : wq! | Ghi bộ đệm vào tệp và thoát khỏi trình chỉnh sửa (ghi đè bảo vệ). |
| : w | Ghi bộ đệm vào tệp và ở trong trình chỉnh sửa. |
| : w! | Ghi bộ đệm vào tệp và ở trong trình chỉnh sửa (ghi đè bảo vệ). |
| : q | Thoát trình chỉnh sửa mà không ghi bộ đệm vào tệp. |
| : q! | Thoát trình chỉnh sửa mà không ghi bộ đệm vào tệp (ghi đè
sự bảo vệ). |
