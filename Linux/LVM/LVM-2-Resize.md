### Thay đổi kích thước


Sau khi tạo, ta có thể chỉnh sửa kích thước  của LV để phù hợp với nhu cầu cũng như lượng dữ liệu. Bước đầu tiên, ta cần phải gỡ bỏ LV đó ra khỏi cây thư mục. 

````
[root@tqhua:~#] umount /dev/vgtest2/lv_test
[root@tqhua:~#] df -h 
Filesystem                         Size  Used Avail Use% Mounted on
udev                               178M     0  178M   0% /dev
tmpfs                               45M  1.4M   43M   4% /run
/dev/mapper/ubuntu--vg-ubuntu--lv   14G  7.2G  5.9G  56% /
tmpfs                              222M     0  222M   0% /dev/shm
tmpfs                              5.0M     0  5.0M   0% /run/lock
tmpfs                              222M     0  222M   0% /sys/fs/cgroup
/dev/loop0                          56M   56M     0 100% /snap/core18/2128
/dev/loop1                          62M   62M     0 100% /snap/core20/1361
/dev/loop2                          56M   56M     0 100% /snap/core18/2284
/dev/loop3                          62M   62M     0 100% /snap/core20/1376
/dev/loop4                          44M   44M     0 100% /snap/snapd/14978
/dev/loop5                          68M   68M     0 100% /snap/lxd/22526
/dev/loop6                          44M   44M     0 100% /snap/snapd/15177
/dev/loop7                          68M   68M     0 100% /snap/lxd/21835
/dev/sda2                          976M  305M  605M  34% /boot
tmpfs                               45M     0   45M   0% /run/user/1000
````

#### Tăng kích thước LV  bằng `lvextend`

`` lvextend -L <độ lớn sau khi tăng> <đường dẫn LV>``

````
[root@tqhua:~#] lvextend -L 600M /dev/vgtest2/lv_test
  Size of logical volume vgtest2/lv_test changed from 500.00 MiB (125 extents) to 600.00 MiB (150 extents).
  Logical volume vgtest2/lv_test successfully resized.
````

#### Giảm kích thước LV  bằng `lvreduce`

`` lvreduce -L <độ lớn sau khi tăng> <đường dẫn LV>``

````
[root@tqhua:~#] lvreduce -L 500M /dev/vgtest2/lv_test
  WARNING: Reducing active logical volume to 500.00 MiB.
  THIS MAY DESTROY YOUR DATA (filesystem etc.)
  Do you really want to reduce vgtest2/lv_test? [y/n]: y
````


#### Tăng/giảm kích thước LV  bằng `lvresize`

`` lvresize -L [+|-]<độ lớn sau khi tăng|giảm> <đường dẫn LV>``

````
[root@tqhua:~#] lvresize -L -100M /dev/vgtest2/lv_test
  WARNING: Reducing active logical volume to 400.00 MiB.
  THIS MAY DESTROY YOUR DATA (filesystem etc.)
  Do you really want to reduce vgtest2/lv_test? [y/n]: y
  Size of logical volume vgtest2/lv_test changed from 500.00 MiB (125 extents) to 400.00 MiB (100 extents).
  Logical volume vgtest2/lv_test successfully resized.
````

````
[root@tqhua:~#] lvreduce -L +100M /dev/vgtest2/lv_test
  Size of logical volume vgtest2/lv_test changed from 400.00 MiB (100 extents) to 500.00 MiB (125 extents).
  Logical volume vgtest2/lv_test successfully resized.
````

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


