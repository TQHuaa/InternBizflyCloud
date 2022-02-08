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
| h | Move cursor left one character. | 
| l | Move cursor right one character. | 
| j | Move cursor down one line (the next line in the text). | 
| k | Move cursor up one line (the previous line in the text). | 
| w | Move cursor forward one word to front of next word. | 
| e | Move cursor to end of current word. | 
| b | Move cursor backward one word. | 
| ^ | Move cursor to beginning of line. | 
| $ | Move cursor to end of line. | 
| gg | Move cursor to the file’s first line. | 
| G | Move cursor to the file’s last line. | 
| nG | Move cursor to file line number n . | 
| Ctrl+B | Scroll up almost one full screen. | 
| Ctrl+F | Scroll down almost one full screen. | 
| Ctrl+U | Scroll up half of a screen. | 
| Ctrl+D | Scroll down half of a screen. | 
| Ctrl+Y | Scroll up one line. | 
| Ctrl+E | Scroll down one line. | 
