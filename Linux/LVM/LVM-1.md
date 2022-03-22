 ### LVM là gì ?

**LVM** (Logical Volume Management) là một công nghệ giúp quản lý các thiết bị lưu trữ dữ liệu trên các hệ điều hành Linux. Công nghệ này cho phép người dùng gom nhóm các ổ cứng vật lý lại và phân tách chúng thành những phân vùng nhỏ hơn nhằm tạo các phân vùng ảo Logical Volume để tăng khả năng lưu trữ.

### Tại sao lại cần LVM? 

LVM đặc biệt hữu ích khi chúng ta sử dụng gần hết lưu lượng của các ổ cứng mà muốn mở rộng không gian lưu trữ trong khi không cần can thiệp quá nhiều lên hệ thống. Một lợi thế lớn của LVM nữa là việc mở rộng các vùng nhớ Logical Volume sẽ không gây gián đoạn tới hoạt động của các dịch vụ trên hệ thống. Có thể thấy, so với phương pháp lưu trữ trên đĩa vật lý truyền thống, LVM mang lại tính linh hoạt hơn nhiều.

### Một số thuật ngữ trong LVM

- **Physical Volume – PV**: Là các partition trên ổ cứng vật lý. 
- **Volume Group – VG**: là tập hợp các PV thành một kho lưu trữ chung.
- **Logical Volume – LV**: là các vùng lưu trữ được tạo ra từ VG bằng cơ chế device mapper.  
- **Physical extent - PE**: PE là đơn vị nhỏ nhất có thể được phân bổ trong VG, được tạo ra bằng cách chia nhỏ các PV.
- **Volume extent - VE** : VE là các đơn vị lưu trữ có kích thước bằng với PE. Mỗi một VE sẽ được ánh xạ tới PE để được tác dụng lưu trữ thực.

Cơ chế device mapping là sự khác biệt của Logical Volume so với các partition trên ổ cứng. Ta có thể thấy sự mapping của LVM ở ảnh dưới :

<img src="https://github.com/TQHuaa/TrainingVCCloud/blob/main/Pics/LVM-1.png">

Hình minh họa LVM (Nguồn: Wikipedia)

## Các chức năng chính của LVM

### Các lệnh của LVM

Trên Linux, chương trình LVM được cung cấp sẵn dưới giao diện dòng lệnh, để sử dụng, ta gõ lệnh **lvm < option>** . Xem chi tiết các option, ta dùng ``lvm help``
````
root@tqhua:~# lvm help
  config          Hiển thị và thao tác thông tin cấu hình
  devtypes        Hiển thị các block device types
  dumpconfig      Hiển thị và thao tác thông tin cấu hình
  formats         Hiển thị các định dạng metadata có sẵn
  help            Trợ giúp cho các lệnh
  fullreport      Hiển thị toàn bộ thông tin về các volume
  lastlog         Display last command's log report
  lvchange        Thay đổi các thuộc tính của LV
  lvconvert       Change logical volume layout
  lvcreate        Tạo LV
  lvdisplay       Hiển thị thông tin về LV
  lvextend        Thêm vùng nhớ vào LV
  lvmchange       With the device mapper, this is obsolete and does nothing.
  lvmconfig       Hiển thị và thao tác thông tin cấu hình
  lvmdiskscan     Hiển thị các partition có thể tạo PV
  lvreduce        Giảm kích thước của LV.
  lvremove        Xoá bỏ LV
  lvrename        Đổi tên LV
  lvresize        Thay đổi kích thước LV
  lvs             Hiển thị thông tin về LV
  lvscan          Hiển thị tất cả LV trên hệ thống
  pvchange        Thay đổi thuộc tính của PV 
  pvresize        Thay đổi kích thước của PV
  pvck            Kiểm tra metadata của PV
  pvcreate        Tạo PV
  pvdata          Hiển thị metadata của PV (Display the on-disk metadata for physical volume(s) )
  pvdisplay       Hiển thị thông tin PV
  pvmove          Di chuyển các extent từ PV này sang PV khác
  lvpoll          Continue already initiated poll operation on a logical volume
  pvremove        Xóa PV
  pvs             Hiển thị thông tin PV
  pvscan          Hiển thị toàn bộ PV
  segtypes        Hiển thị toàn bộ segment types
  systemid        Display the system ID, if any, currently set on this host
  tags            List tags defined on this host
  vgcfgbackup     Sao lưu thông tin cấu hình VG
  vgcfgrestore    Khôi phục thông tin cấu hình VG
  vgchange        Thay đổi thuộc tính VG
  vgck            Check the consistency of volume group(s)
  vgconvert       Thay đổi metadata format của VG
  vgcreate        Tạo VG
  vgdisplay       Hiển thị thông tin VG
  vgexport        Unregister volume group(s) from the system
  vgextend        Thêm PV vào VG
  vgimport        Register exported volume group with system
  vgimportclone   Import a VG from cloned PVs
  vgmerge         Gộp VG
  vgmknodes       Create the special files for volume group devices in /dev
  vgreduce        Gỡ PV khỏi VG
  vgremove        Xóa VG
  vgrename        Đổi tên VG
  vgs             Hiển thị thông tin về VG
  vgscan          Hiển thị toàn bộ VG
  vgsplit         Di chuyển PV tới một VG khác 
  version         Hiển thị thông tin phiên bản

````

Xem các lệnh liên quan đến xử lý PV, ta chú ý tiền tố `pv*` : 
````
  pvchange        Thay đổi thuộc tính của PV 
  pvresize        Thay đổi kích thước của PV
  pvck            Kiểm tra metadata của PV
  pvcreate        Tạo PV
  pvdata          Hiển thị metadata của PV (Display the on-disk metadata for physical volume(s) )
  pvdisplay       Hiển thị thông tin PV
  pvmove          Di chuyển các extent từ PV này sang PV khác
  pvremove        Xóa PV
  pvs             Hiển thị thông tin PV
  pvscan          Hiển thị toàn bộ PV
````

Xem các lệnh liên quan đến xử lý VG, ta chú ý tiền tố `vg*` : 
````
  vgcfgbackup     Sao lưu thông tin cấu hình VG
  vgcfgrestore    Khôi phục thông tin cấu hình VG
  vgchange        Thay đổi thuộc tính VG
  vgck            Check the consistency of volume group(s)
  vgconvert       Thay đổi metadata format của VG
  vgcreate        Tạo VG
  vgdisplay       Hiển thị thông tin VG
  vgexport        Unregister volume group(s) from the system
  vgextend        Thêm PV vào VG
  vgimport        Register exported volume group with system
  vgimportclone   Import a VG from cloned PVs
  vgmerge         Gộp VG
  vgmknodes       Create the special files for volume group devices in /dev
  vgreduce        Gỡ PV khỏi VG
  vgremove        Xóa VG
  vgrename        Đổi tên VG
  vgs             Hiển thị thông tin về VG
  vgscan          Hiển thị toàn bộ VG
  vgsplit         Di chuyển PV tới một VG khác 
````

Xem các lệnh liên quan đến xử lý LV, ta chú ý tiền tố `lv*` : 
````
  lvchange        Thay đổi các thuộc tính của LV
  lvconvert       Change logical volume layout
  lvcreate        Tạo LV
  lvdisplay       Hiển thị thông tin về LV
  lvextend        Thêm vùng nhớ vào LV
  lvreduce        Giảm kích thước của LV.
  lvremove        Xoá bỏ LV
  lvrename        Đổi tên LV
  lvresize        Thay đổi kích thước LV
  lvs             Hiển thị thông tin về LV
  lvscan          Hiển thị tất cả LV trên hệ thống
  lvpoll          Continue already initiated poll operation on a logical volume
````

### Thao tác tạo

Các bước sử dụng LVM cơ bản gồm: 
 
-  Bước 1 : Tạo PV.
-  Bước 2 : Tạo VG.
-  Bước 3 : Tạo LV.
-  Bước 4 : Tạo filesystem cho LV.
-  Bước 5 : Mount LV vào cây thư mục và sử dụng.

#### Tạo Physical Volume

Để tạo được physical volume trước tiên ta cần kiểm tra xem ổ đĩa nào đang còn trống bằng lệnh `lvmdiskscan` :

````
[root@tqhua:~#] lvmdiskscan

  /dev/md0   [       1.99 GiB] 
  /dev/loop1 [     <55.51 MiB] 
  /dev/md1   [    1022.00 MiB] 
  /dev/loop2 [      61.89 MiB] 
  /dev/sda2  [       1.00 GiB] 
  /dev/loop3 [      61.89 MiB] 
  /dev/sda3  [     <13.00 GiB] LVM physical volume
  /dev/loop4 [      67.24 MiB] 
  /dev/loop5 [      67.92 MiB] 
  /dev/loop6 [     <43.59 MiB] 
  /dev/loop7 [     <43.63 MiB] 
  /dev/loop8 [     <55.52 MiB] 
  /dev/sdd1  [    1023.00 MiB] LVM physical volume
  /dev/sde   [       1.00 GiB] LVM physical volume
  0 disks
  11 partitions
  1 LVM physical volume whole disk
  2 LVM physical volumes

```` 

Khi đã có thông tin về các ổ đĩa, ta có thể lựa chọn một ổ đĩa trống để tạo PV. Ở đây, mình chọn `/dev/md1` là ổ raid1 đã tạo sẵn. 
Ta sử dụng lệnh ``pvcreate`` theo cú pháp : ``pvcreate /dev/*tên phân vùng*``. Màn hình sẽ hiển thị thông báo tạo thành công.

````
[root@tqhua:~#] pvcreate /dev/md1
  Physical volume "/dev/md1" successfully created.

````

Để kiểm tra tạo được PV chưa, ta sử dụng lệnh ``pvs`` :
          
````
[root@tqhua:~#] pvs
    PV         VG        Fmt  Attr PSize    PFree   
  /dev/md1             lvm2 ---  1022.00m 1022.00m
  /dev/sda3  ubuntu-vg lvm2 a--   <13.00g       0 
  /dev/sdd1  ubuntu-vg lvm2 a--  1020.00m       0 
  /dev/sde   vgtest    lvm2 a--  1020.00m 1020.00m

````

Kết quả cho thấy đĩa `/dev/md1` đã được tạo PV nhưng chưa có trong VG nào cả.

#### Tạo một Group volume

Để tạo một VG và thêm PV vào luôn, ta sử dụng lệnh ``vgcreate`` theo cú pháp: 

``vgcreate *ten_group* /dev/*tên phân vùng 1* [/dev/*tên phân vùng 2*]``

Mình sẽ tạo VG tên là *vgtest2* làm ví dụ.

````
[root@tqhua:~#] vgcreate vgtest2 /dev/md1 
   Volume group "/dev/md1" successfully created.

````

Ta sử dụng lệnh ``vgs`` để kiểm tra xem group volume.

````
[root@tqhua:~#] vgs
  VG        #PV #LV #SN Attr   VSize    VFree   
  ubuntu-vg   2   1   0 wz--n-   13.99g       0 
  vgtest      1   0   0 wz--n- 1020.00m 1020.00m
  vgtest2     1   0   0 wz--n- 1020.00m 1020.00m

````
          
#### Tạo một Logical volume

Sau khi tạo VG và thêm các PV vào, ta có thể sử dụng vùng dung lượng trong VG để chia thành các LV với câu lệnh:  

``lvcreate -L *size_volume* -n *ten logical* *tên group volume*``

````
[root@tqhua:~#] lvcreate -L 500M -n lv_test vgtest2
Logical volume "lv_test" successfully created.
````

Để kiểm tra logical volume thì ta sử dụng lệnh ``lvs``
````
[root@tqhua:~#] lvs
  LV        VG        Attr       LSize   Pool Origin Data%  Meta%  Move Log Cpy%Sync Convert
  ubuntu-lv ubuntu-vg -wi-ao----  13.99g                                                    
  lv_test   vgtest2   -wi-a----- 500.00m                                                    
````

Màn hình hiển thị lv_test tức là ta đã tạo thành công.

#### Tạo một Filesystem

Mình sẽ tạo file system có định dạng ext4 ở LV *lv_test*. Để tạo filesystem định dạng ext4, ta sử dụng `mkfs.ext4`. 

````
[root@tqhua:~#] mkfs.ext4 /dev/vgtest2/lv_test
  Creating filesystem with 128000 4k blocks and 128000 inodes 

  Allocating group tables: done
  Writing inode tables: done 
  Creating journal (4096 blocks): done
  Writing supreblocks and filesystem accounting infomation: done                                                    
````

Sau khi tạo filesystem, ta có thể mount nó vào cây thư mục và sử dụng.

````
[root@tqhua:~#] mount /dev/vgtest2/lv_test /mnt/ 
[root@tqhua:~#] df
Filesystem                        1K-blocks    Used Available Use% Mounted on
udev                                 181672       0    181672   0% /dev
tmpfs                                 45332    1420     43912   4% /run
/dev/mapper/ubuntu--vg-ubuntu--lv  14375944 7502812   6133768  56% /
tmpfs                                226656       0    226656   0% /dev/shm
tmpfs                                  5120       0      5120   0% /run/lock
tmpfs                                226656       0    226656   0% /sys/fs/cgroup
/dev/loop0                            56832   56832         0 100% /snap/core18/2128
/dev/loop1                            63488   63488         0 100% /snap/core20/1361
/dev/loop2                            56960   56960         0 100% /snap/core18/2284
/dev/loop3                            63488   63488         0 100% /snap/core20/1376
/dev/loop4                            44672   44672         0 100% /snap/snapd/14978
/dev/loop5                            69632   69632         0 100% /snap/lxd/22526
/dev/loop6                            44800   44800         0 100% /snap/snapd/15177
/dev/loop7                            68864   68864         0 100% /snap/lxd/21835
/dev/sda2                            999320  311744    618764  34% /boot
tmpfs                                 45328       0     45328   0% /run/user/1000
/dev/mapper/vgtest2-lv_test          479560     768    442952   1% /mnt                                           
````

