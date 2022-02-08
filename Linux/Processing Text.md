# File-Combining Commands 

Các lệnh File-Combining dùng để tập hợp các văn bản ngắn gọn lại với nhau.

## CAT 

Giả sử ta có 2 file text chứa nội dung và giờ ta muống gộp nội dung 2 files vào chung 1 file. Ta sẽ làm điều đó với lệnh cat ( concatenate).

``~$ cat file1.txt file2.txt > file3.txt``

Ta còn có thể dùng cat như một lệnh để đọc file có nội dung vừa phải như sau:

``~$ cat file3.txt``

Lệnh cat có nhiều option khác nhau đễ hỗ trợ ta thay đổi đôi chút text file khi tiến hành nối file:
- Nếu ta muốn xem dòng kết thúc ở đâu ta sử dụng option ``-E (end)``, hệ thống sẽ thêm ký hiệu ``$`` vào mỗi cuối dòng.
- Đánh số mỗi dòng với option ``-n (number line)``, option ``-b (nonblank)`` cũng có chức năng tương tự những dòng trống sẽ không được đánh dấu.
  <img src="![image](https://user-images.githubusercontent.com/79156398/152914211-3f47f893-a1da-4fee-bc92-55193c6c4a24.png)">
- Gộp nhiều dòng trống lại thành 1 dòng trống duy nhất với option ``-s``.

## JOIN

Lệnh cat giúp ta nối file theo vertival (hàng dọc), lệnh join thì ngược lại giúp ta nối file theo horizon (hàng ngang). Mặc định join dùng field đầu tiên làm key để ghép 2 file lại với nhau.

``~$ join list1.txt list2.txt``

## PASTE

Lệnh paste dùng để nối dòng với dòng, cách nhau bởi TAB, và không gộp chung key như join.

``~$ paste list1.txt list2.txt``

# File-Transforming Commands 

Transforming file không nhắm đến thay đổi nội dung file mà thay đổi nội dung được xuất ra stdout để pipe đến 1 program khác.

## SPLIT

Lệnh ``split`` thường được sử dụng để tách file lớn thành các phần nhỏ hơn. Cú pháp:

``split [ OPTION ]... [ INPUT [ PREFIX ]]``

````
$ cat fourtytwo.txt
42
fourty two
quarante deux
zweiundvierzig
forti to 
````

**Các Option:**
- Tách file theo số lượng dòng:
  ``$ split -l 3 fourtytwo.txt split42`` //tách file fourtytwo.txt cứ mỗi 3 dòng và lưu vào các file tên split42** (** sắp xếp theo thứ tự alphabet từ aa,ab,...)

# File-Formatting Commands 

Các lệnh này được sử dụng để định dạng dữ liệu dạng văn bẳn trong file.

## SORT 

Lệnh ``sort`` được sử dụng để sắp xếp các dòng của tệp văn bản theo thứ tự tăng dần hoặc giảm dần, theo một khoá sắp xếp. Khóa sắp xếp mặc định là thứ tự của các ký tự ASCII (theo thứ tự bảng chữ cái). Cú pháp của lệnh ``sort``:

``sort [ OPTION ]... [ FILE ]... ``

**Các Option:**
  - Sắp xếp các dòng trong tệp, theo các ký tự ở đầu mỗi dòng : ``sort <file>``
  - Sắp xếp các dòng theo thứ tự ngược lại : ``sort -r <file>``
  - ``-n``, ``--numeric-sort`` : Sắp xếp số
  - ``-R``, ``--random-sort``: sắp xếp random
  
## UNIQ

Lệnh uniq dùng để bỏ các dòng liên tiếp trùng lặp trong một tệp văn bản. Tuy nhiên, điều kiện trùng của lệnh ``uniq`` là các từ phải xếp liên tiếp nhau. Cú pháp lệnh uniq: 

``uniq [OPTION]... [INPUT [OUTPUT]]``

**Các Option chính:** 
   - -d, --repeated
             In các nhóm từ bị lọc trùng
   - -D     In các từ bị lọc trùng
   - -u, --unique
              Chỉ in các từ 

## NL 

Được sử dụng để đánh dòng văn bản. Cú pháp: 
``nl [ OPTION ]... [ FILE ]...``

Ví dụ : 
````
$ nl ContainsBlankLines.txt
 1 Alpha
 2 Tango
  
 3 Bravo
 4 Echo
  
  
 5 Foxtrot 
````
  
**Các Option chính:**  
  - -ba : đánh số cả dòng trống

## TAC

````
~$tac file1.txt
3
2
1
~$cat file1.txt
1
2
3
````

Giống như lệnh cat, Nhưng in ngược lại các dòng của file1.txt, từ dòng cuối cùng đến dòng đầu tiên. Cú pháp: 
`` tac [OPTION]... [FILE]...``

**Các Option chính:**  
- -b : Gắn dấu phân cách dòng trước mỗi dòng đầu ra thay vì sau.
- -NS : Sử dụng STRING làm dấu phân tách dòng thay vì một dòng mới.

#  File-Viewing Commands 

## HEAD

Lệnh ``head`` dùng để xem những dòng đầu của tệp tin (theo mặc định là 10 dòng đầu tiên). Chúng ta có thể thay đổi số dòng bằng cách thêm -n vào sau lệnh ``head``. Cú pháp lệnh ``head``:

`` head [ OPTION ]... [ FILE ]...``

**Các Option chính:**
  - -c, --byte=[-]n: In số byte n đầu tiên của mỗi tệp
  - -n, --lines=[-]n: In số dòng n đầu tiên của mỗi tệp
 
## TAIL 

Lệnh ``tail`` dùng để xem những dòng đầu của tệp tin (theo mặc định là 10 dòng). Lệnh ``tail`` rất hữu ích khi khắc phục sự cố tệp nhật ký. Cú pháp lệnh ``tail``:

``tail [OPTION]... [FILE]...``

**Các Option chính:**
  - -n, --lines=[-]n: In số dòng n cuối cùng của mỗi tệp
  - -n, --lines=[+]n: In tất cả các dòng từ n về sau
  - -c, --byte=[-]n: In số byte n đầu cuối cùng mỗi tệp
  
## LESS or MORE  

*"less is more"*, như câu nói vui trên, tác dụng của hai lệnh gần như là giống nhau mặc dù đều được đề cập trong ``man``. Lệnh less dùng mở một tệp để đọc tương tác, cho phép di chuyển lên xuống và tìm kiếm. Cú pháp: 

Lệnh more
``more [ OPTION ] FILE [...] ``

Lệnh less
``less [ OPTION ] FILE [...] ``

Trang lên trang xuống:

  - Phím Space: di chuyển xuống trang mới
  - Phím b: di chuyển lên lại trang phía trên

Lệnh less có thể dùng phím mũi tên trên bàn phím để scroll lên xuống.

Di chuyển đến cuối, bắt đầu tập tin:

  - Phím G: di chuyển đến cuối tập tin
  - Phím g: di chuyển đến đầu tập tin

Tìm kiếm một chuỗi

``/{chuỗi}``
Hay

``?{chuỗi}``
Theo dõi đầu ra của tệp hiện đang mở:

``Phím F``
Mở tệp hiện tại trong trình chỉnh sửa:

``Phím v``
Thoát tệp hiện tại:

``Phím q``

Điểm khác biệt: Điểm khác biệt giữa less và more là less cho phép cuộn ngược lên các trang dữ liệu đã đọc, còn more thì chỉ có thể đọc từ đầu tới cuối. Lệnh less có thể dùng phím mũi tên trên bàn phím để scroll lên xuống, lệnh more không có chức năng này.

#  File-Summarizing Commands 

## CUT

Lệnh cut được sử dụng thao tác với tệp dựa trên cột và được thiết kế để trích xuất các cột cụ thể. Dấu phân cách cột mặc định là ký tự tab.
Ví dụ 1: Cắt mười sáu ký tự đầu tiên của mỗi dòng STDIN:
````
[root@test1 ~]# echo "This is a filetest" | cut -c 1-16
This is a filete
````

**Các Option chính:**
  - -f( --fields=LIST) – Chọn bằng cách chỉ định một trường, một tập hợp các trường hoặc một phạm vi trường. Đây là tùy chọn được sử dụng phổ biến nhất.
  - -b( --bytes=LIST) – Chọn bằng cách chỉ định một byte, một tập hợp các byte hoặc một dải byte.
  - -c( --characters=LIST) – Chọn bằng cách chỉ định một ký tự, một bộ ký tự hoặc một dải ký tự.

Ví dụ: 
  - Ta có file test.txt 

  ````
  245:789 4567    M:4540  Admin   01:10:1980
  535:763 4987    M:3476  Sales   11:04:1978
  ````
  
  Để hiển thị trường thứ nhất và thứ 3, ta dùng lệnh : 
  ``cut test.txt -f 1,3``
  
  Kết quả :
  ````
  245:789 M:4540
  535:763 M:3476
  ````

## WC
Lệnh ``wc`` cũng có tác dụng giống như lệnh ``cut`` nhưng xử lý đến từ, byte hoặc dòng. Cú pháp :
``wc [ OPTION ]... [ FILE ]...``

**Các Option chính:**

  - -l	Hiển thị số lượng dòng
  - -c	Hiển thị số lượng byte
  - -w	Hiển thị số lượng từ

# Tài liệu tham khảo 
https://blogd.net/linux/cach-dung-lenh-sort-uniq-paste-join-split/#4-l%E1%BB%87nh-split

https://vietnamtutor.com/kham-pha-command-line-tren-linux-phan-3-xu-ly-text-bang-filter-trong-linux-cat-join-paste-sort-head-tail-wc/

https://hocdevops.com/commands/lenh-cut-trong-linux/#Cach_su_dung

LPIC-1

