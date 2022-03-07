
![image](https://user-images.githubusercontent.com/79156398/155563872-413b6b6e-5998-42e9-afad-fcc1e171cebb.png)

![image](https://user-images.githubusercontent.com/79156398/155564209-28ab04f6-86a8-492e-bc56-764fa46e6b17.png)

![image](https://user-images.githubusercontent.com/79156398/155565222-c76fdbff-30b5-4b84-85b9-ecf9f7b54e0b.png)

# Tạo filesystem 

``mkfs`` là một công cụ để tạo file system. Hôm nay, mình sẽ thực hành tạo filesystem trên Ubuntu server 20.04. 

## Tạo disk partition

Kiểm tra xem các ổ đĩa trên hệ thống :  ``sudo fdisk -l | grep sd``
Tạo một partition mới (xem tại [đây](https://github.com/TQHuaa/TrainingVCCloud/blob/main/Linux/Lab/Tao%20RAID.md#t%E1%BA%A1o-ph%C3%A2n-v%C3%B9ng-cho-%E1%BB%95-%C4%91%C4%A9a)) : ``sudo fdisk /dev/sde``
Kiểm tra partions table sau khi tạo

## Tạo Filesystem
Tạo filesystem ext4 bằng ``mkfs`` : ``sudo mkfs.ext4 /dev/sde1``

## Tham khảo





