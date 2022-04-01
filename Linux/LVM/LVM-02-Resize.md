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
