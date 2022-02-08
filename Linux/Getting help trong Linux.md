## Khái niệm
Lệnh man trong linux được sử dụng để tìm kiếm, xem thông tin về các lệnh trên hệ thống

## Cách dùng 

**Tìm kiếm** 

Tìm kiếm theo từ khóa : ``man -f <từ khóa>``. Kết quả trả về tên lệnh cùng với section number, chức năng tương ứng.
  Ví dụ: ```
  ubuntu@ip-172-31-32-136:~$ man -k passwd
  chgpasswd (8)        - update group passwords in batch mode
  chpasswd (8)         - update passwords in batch mode
  gpasswd (1)          - administer /etc/group and /etc/gshadow
  grub-mkpasswd-pbkdf2 (1) - generate hashed password for GRUB
  openssl-passwd (1ssl) - compute password hashes
  pam_localuser (8)    - require users to be listed in /etc/passwd
  passwd (1)           - change user password
  passwd (1ssl)        - compute password hashes
  passwd (5)           - the password file
  update-passwd (8)    - safely update /etc/passwd, /etc/shadow and /etc/group
  ```
Xem thông tin đầy đủ của một lệnh: ``man -s <section number> <tên lệnh>``

Để xem đầy đủ hơn về các tính năng của lệnh man, truy cập vào man page với lệnh ``man man``

## Tài liệu tham khảo 
LPIC-1
