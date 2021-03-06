## Preparation of Node
#### Increase root partion from 3Gb to 60Gb
```
# fdisk -cu /dev/xvdb
```
* To Create new partition Press **n**.
* Choose primary partition use **p**.
* Choose which number of partition to be selected to create the primary partition.
* Press **1** if any other disk available.
* Change the type using **t**.
* Type **8e** to change the partition type to Linux LVM.
* Use **p** to print the create partition ( here we have not used the option).
* Press **w** to write the changes
*or trying to do in one single command:
```
# (echo n; echo p; echo 3; echo; echo; echo t; echo 3; echo 8e; echo p; echo w) | sudo fdisk -cu /dev/xvdb
```
Creating physical volume manager
``` 
# sudo pvcreate /dev/xvdb3
```
Extending current volume group
``` 
sudo vgextend vg_main /dev/xvdb3
```
Adding more blocks to logical volume
```
# sudo lvextend -l +1503 /dev/vg_main/lv_root
# sudo resize2fs /dev/vg_main/lv_root
```

#### Enabling and disabling repositories 
```
# sudo yum install -y yum-utils
# sudo yum-config-manager --disable ol6_UEKR3_latest
# sudo yum-config-manager --enable ol6_UEKR4
# sudo yum-config-manager --enable ol6_addons
```
#### Installing requiered packages and reset
```
# sudo yum install -y nano git wget curl docker-engine
# sudo reboot
```

#### Update repository
```
# cd /etc/yum.repos.d
# sudo wget https://raw.githubusercontent.com/renecloud/HOL-OOWBR/master/files/ol6_uekr4.repo
```
