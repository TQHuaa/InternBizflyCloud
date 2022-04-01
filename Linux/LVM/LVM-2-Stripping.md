
### Striping

Striping là cơ chế ánh xạ của LVM cho phép ghi dữ liệu lên nhiều đĩa khác nhau nhằm mục đích tăng hiệu năng ghi dữ liệu lên các đĩa. Nôm na thì nó giống như RAID-0 vậy. 

<img src=https://www.google.com/imgres?imgurl=https%3A%2F%2Fnetworkencyclopedia.com%2Fwp-content%2Fuploads%2F2019%2F08%2Fraid-0-disk-striping-1024x951.jpg&imgrefurl=https%3A%2F%2Fnetworkencyclopedia.com%2Fraid-0%2F&tbnid=9nMoI2bZm2ki4M&vet=12ahUKEwi4kLyLp-r2AhUNA6YKHSufD7MQMygBegUIARDWAQ..i&docid=piyX0w5M_FvC6M&w=995&h=924&q=raid%200&ved=2ahUKEwi4kLyLp-r2AhUNA6YKHSufD7MQMygBegUIARDWAQ >

Để tạo được Striped LV, trước tiên chúng ta cần tạo một VG có chứa 2 disk đã tạo PV là ``/dev/sde`` và ``/dev/md1``.

````
[root@tqhua:~#] vgcreate vgtest /dev/sde /dev/md1
  Volume group "vgtest" successfully created
````

Khi màn hình console thông báo tạo thành công, ta tiến hành tạo Striped LV bằng ``lvcreate`` với tùy chọn ``-i``.

````
[root@tqhua:~#] lvcreate -i 2 -L 500M -n lv_striped /dev/vgtest
  Using default stripesize 64.00 KiB.
  Rounding size 500.00 MiB (125 extents) up to stripe boundary size 504.00 MiB (126 extents).
  Logical volume "lv_striped" created.
````

Với ``-i`` = 2, việc ghi dữ liệu sẽ được chia đều lên 2 đĩa có trong VG ``vgtest`` mà ta vừa tạo.

Như vậy là ta đã tạo xong được Striped LV. Kiểm tra bằng lvs, ta sẽ thấy LV ``lv_striped`` gồm 2 đĩa tạo thành.

````
[root@tqhua:~#] lvs -a -o +devices
  LV          VG        Attr       LSize   Pool Origin Data%  Meta%  Move Log Cpy%Sync Convert Devices                
  ubuntu-lv   ubuntu-vg -wi-ao----  13.99g                                                     /dev/sda3(0)           
  ubuntu-lv   ubuntu-vg -wi-ao----  13.99g                                                     /dev/sdd1(0)           
  lv_striped vgtest    -wi-a----- 504.00m                                                     /dev/md1(0),/dev/sde(0)

````

Trong đó: 
	- ``-a`` : All - Hiển thị tất cả các LV.
	- ``-o`` : Output - Tùy chọn hiển thị output.

Kiểm tra lại dung lượng của các PV ``/dev/md1`` và ``/dev/sde``, hai đĩa có dung lượng đã sử dụng bằng nhau là 252m. Đây cũng là dung lượng đã được dùng để phân bổ cho Striped LV ta đã tạo ở trên.

````
[root@tqhua:~#] pvs
  PV         VG        Fmt  Attr PSize    PFree  
  /dev/md1   vgtest    lvm2 a--  1020.00m 768.00m
  /dev/sda3  ubuntu-vg lvm2 a--   <13.00g      0 
  /dev/sdd1  ubuntu-vg lvm2 a--  1020.00m      0 
  /dev/sde   vgtest    lvm2 a--  1020.00m 768.00m

````


