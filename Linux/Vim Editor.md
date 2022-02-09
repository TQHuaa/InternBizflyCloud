# Vim cơ bản

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

# Vimtutor

Phần này sẽ trình bày về *vimtutor*, một bản hướng dẫn cơ bản cho người sử dụng Vim. Vimtutor được chia thành 7 bài học với các chức năng chính của Vim: 
 - Lesson 1 - Moving the Cursor, Editing A File, Exiting, Insertion, Deletion, Appending.
 - Lesson 2 - Moving Cursor, Deletion and Undo.
 - Lesson 3 - Replace, Delete.
 - Lesson 4 - Moving, Search & Replace.
 - Lesson 5 - Excute External Command.
 - Lesson 6 - Copy && Some Options.
 - Lesson 7 - Helper in VIM.

## Lesson 1 - Moving the Cursor, Editing A File, Exiting, Insertion, Deletion, Appending.

1.1 - Moving the Cursor (In Command Mode ESC) Di chuyển trỏ chuột trong VIM (Có thể dùng các phím mũi tên nhưng không khuyến khích)

                            k(up)
                            ^                                  
                            |                                               
                 h(left) <--+--> l(right)                                              
                            |                                              
                            v                                             
                            j (down)  
                            
1.2 - Opening and Exiting VIM

Start vim from the shell prompt type
``vim FILENAME (Hoăc vi FILENAME)``
To Exit vim
``:q!`` to trash all changes. ``:wq`` to save the changes.

1.3 - Delete character at the cursor type: ``x``

1.4 - ``i`` để insert before cursor. ``a`` để insert after cursor. ``A`` (``Shift a``) để append after the line.

## Lesson 2 - Moving Cursor, Deletion and Undo.

type ``de`` to delete to the end of current word. type ``dw`` to delete until the start of next word. type ``dd`` to delete the line.

``de``,``dw``,``dd`` có thể dùng kèm với số để xóa nhanh nhiều từ, ví dụ ``d2w``, ``d3e``, ``2dd``…

type ``d$`` to delete to the end of the line.

type ``2w`` to move the cursor two words forward. type ``3e`` to move the cursor to the end of the third word forward. type ``0`` to move to the start of the line. type ``$`` to move to the end of the line. type ``b`` - opposite with ``w``

type ``u`` to undo the last commands, ``U`` to fix a whole line. type ``Ctrl+R`` to redo the undo command.

## Lesson 3 - Replace, Delete.

Những lệnh liên quan đến deletion như ``x``, ``dd``, ``dw``, ``de``… đều được vim đưa nội dung đã xóa vào register (giống Clipboard vậy)… và bạn có thể dùng ``p`` để dán nội dung trong register vào nơi bạn muốn.

``r`` để replace ký tự tại cursor.

``ce`` và ``cw`` để replace từ hoặc phần còn lại của từ tại cursor. (``ce`` là kết hợp giữa ``de`` và ``i``)

``c$`` là kết hợp giữa ``d$`` và ``i`` - Xóa phần còn lại của dòng.

## Lesson 4 - Moving, Search & Replace.

``Ctrl+G`` để biết thêm thông tin về File hiện hành: Tên file, vị trí hiện tại trong file (số dòng)

``G`` (``shift G``) để di chuyển đến dòng cuối của file (tương tự ``:$``)

``gg`` để di chuyển đến dòng đầu tiên của file (tương tự ``:0``)

``:line_number`` để di chuyển đến dòng cụ thể trong File. (Tương tự việc gõ ``line_numer G`` - ``Shift G``)

``/từ_cần_tìm`` - Tìm kiếm trong vim, cursor sẽ nhảy đến từ đầu tiên mà nó tìm thấy. ``n`` để di chuyển next, ``N`` để đến previous trong lúc tìm kiếm

(nếu ``/từ_cần_tìm`` là đi tới thì ``?từ_cần_tìm`` là tìm kiếm quay lui.)

``Ctrl+O`` to go back to where you came from.

``Ctrl+I`` to go forward (ngược với ``Ctrl+O``)

Matching parenthesis or bracket:

Khi đặt cursor trên các ký tự như ``(``, ``[`` hoặc ``{`` và gõ command ``%`` thì cursor sẽ được nhảy đến phần đóng hoặc mở thẻ tương ứng với nó - rất hữu ích trong lập trình và trong lúc cấu hình hệ thống.

``:s/old/new/g`` để Tìm kiếm và thay thế chuỗi ``old`` bằng chuỗi ``new``.

Chỉ thị ``g`` cho phép thay thế toàn bộ ocurrences của từ đang tìm trong dòng hiện tại. (Bỏ chỉ thị ``g`` đi nếu chỉ muốn thay thế First occurrence).

``:#,#s/old/new/g`` Search & Replace tại những dòng cụ thể.

``:%s/old/new/g`` - Search & Replace mọi ocurrences trong toàn bộ nội dung của File.

``:%s/old/new/gc`` Search & Replace mọi ocurrences trong toàn bộ nội dung của File nhưng có prompt để xác định muốn replace occurence đó hay không.

## Lesson 5 - Excute External Command.

``:!`` cho phép bạn nhập và thực thi external command (Các lệnh ngoài vim như lệnh của shell) trực tiếp trong VIM. (Rất hữu ích đối với Developer)

``:w`` FILE_NAME - Giống Save As ở các Editor thông thường, Lưu lại File hiện tại với Tên khác.

``v`` để chuyển sang Visual Selection mode, bạn có thể select nhiều dòng một cách trực quan trong mode này.

``:r FILE_NAME`` để chèn nội dung của một file khác vào cursor.

``:r !ls`` chèn output của lệnh ls vào cursor

## Lesson 6 - Copy && Some Options.

``o`` - Open a line below the cursor and place you in Insert mode.

``O`` - Open a line above the cursor and place you in Insert mode.

``R`` - Nếu ``r`` có tác dụng replace từng ký tự thì ``R`` sẽ chuyển bạn sang hẳn Replace Mode. (Nhấn ESC để thoát Replace Mode nếu không cần)

``y`` để copy nội dung của dòng vào register và ``p`` để dán. (Các lệnh liên quan đến Deletion như ``dw``, ``de``, ``dd``,``d$``…thực ra tương tự lệnh cut)

``y`` kết hợp với Visual Mode ``v`` để select và copy highlighted text.

``y`` đóng vai trò là operator như ``d``, nghĩa là bạn có thể kết hợp với số lượng ở trước ``2y``, ``3y`` để copy nhiều dòng, kết hợp với ``w``,``e``,``y`` - ``yw``, ``y2w``…

 - ``:set ic`` - Set Option Ignore case cho các lệnh tìm kiếm

 - ``:set ts=4`` - Set Tab indent = 4

 - ``:set nu`` - Set hiển thị line number

 - Để tắt option đã set, thêm tiền tố no, ví dụ: :set nonu

 - ...

## Lesson 7 - Helper in VIM.

Nếu gặp khó khăn trong quá trình sử dụng vim, nếu không nhớ lệnh này có ý nghĩa gì thì ta có thể mở help ngay trong vim. ``:help``, ``:help lệnh_cần_biết``

``Ctrl+W`` để chuyển qua lại giữa các cửa sổ (Nếu ta Split vim thành nhiều panel)

File cấu hình của vim là:

``~/.vimrc`` - là nơi chứa các cấu hình của vim. Ta có thể edit file .vimrc và copy nội dung file vimrc_example.vim bằng lệnh:

``:r $VIMRUNTIME/vimrc_example.vim``

Nhắc lệnh trong vim:
``:set nocp``

Khi gõ một lệnh, Ta có thể nhấn ``Ctrl+D`` để hiển thị hết danh sách các lệnh bắt đầu bằng ký tự ta gõ, nhấn ``TAB`` để auto complete (tương tự như TAB trong Terminal của Linux).
 

# Tài liệu tham khảo

http://notes.viphat.work/vimtutor
LPIC-1
