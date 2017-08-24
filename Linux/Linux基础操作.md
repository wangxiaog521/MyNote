## Linux添加用户
```shell
# 显示用户信息，以及已加入的用户组
id
# 添加一个用户
useradd 
# 添加用户并制定UID，GUID和root用户组
useradd -u 505 -g 505 -G root log 
# log加入root组
usermod -G root log 
# 添加log用户组
groupadd -g 505 log 
```

## iterm2断开连接
```shell
# mac下在~/.ssh/config里添加如下：
ServerAliveInterval 50
```

## 个性化.bash_profile
```shell
# PS1设置
export PS1='\n\e[1;37m[\e[m\e[1;32m\u\e[m\e[1;33m@\e[m\e[1;35m\H\e[m \e[4m`pwd`\e[m\e[1;37m]\e[m\e[1;36m\e[m\n\$ '
```

## find命令
```shell
# 查找30天以内20天以外的文件
find . -mtime -30 +20
```

## 网络配置
```shell
# 添加一条路由规则
route add –net 11.0.0.0 netmask 255.0.0.0 gw 10.228.20.1
```

## 分配存储
### 1. check the allocated disk
```shell
# df -h
Filesystem            Size  Used Avail Use% Mounted on
/dev/sda2              95G   15G   76G  16% /
/dev/sda1             247M   42M  193M  18% /boot
/dev/sda3             9.9G  534M  8.9G   6% /tmp
/dev/sda5             9.9G  1.2G  8.2G  13% /home
tmpfs                  95G  336K   95G   1% /dev/shm
# ls -ltr /dev/sd*
brw-r----- 1 root disk 8,  2 Aug 16 12:00 /dev/sda2
brw-r----- 1 root disk 8,  1 Aug 16 12:00 /dev/sda1
brw-r----- 1 root disk 8,  0 Aug 16 20:00 /dev/sda
brw-r----- 1 root disk 8,  4 Aug 16 20:00 /dev/sda4
brw-r----- 1 root disk 8,  3 Aug 16 20:00 /dev/sda3
brw-r----- 1 root disk 8, 16 Aug 16 20:00 /dev/sdb # which is not mounted
```

### 2. using command parted to create space /dev/sdb1
```shell
# parted /dev/sdb
GNU Parted 1.8.1
Using /dev/sdb
Welcome to GNU Parted! Type 'help' to view a list of commands.
(parted) p # print partition info                                                                       

Model: LSI LSI (scsi)
Disk /dev/sdb: 3832GB
Sector size (logical/physical): 512B/512B
Partition Table: gpt

Number  Start  End  Size  File system  Name  Flags

(parted) mkpart # create partition
Partition name?  []? primary                                              
File system type?  [ext2]? ext3
Start? 0                                                                  
End? 3832GB
(parted) p # print partition info                                                               

Model: LSI LSI (scsi)
Disk /dev/sdb: 3832GB
Sector size (logical/physical): 512B/512B
Partition Table: gpt

Number  Start   End     Size    File system  Name     Flags
 1      17.4kB  3832GB  3832GB               primary       

(parted) quit                                                             
Information: Don't forget to update /etc/fstab, if necessary.

#ls -ltr /dev/sdb*
brw-r----- 1 root disk 8, 16 Aug 16 20:00 /dev/sdb
brw-r----- 1 root disk 8, 17 Aug 16 20:00 /dev/sdb1
```

### 3. using mkfs to create ext3 filesytem and mount it
```shell
# mkfs -t ext3 /dev/sdb1
mke2fs 1.39 (29-May-2006)
Filesystem label=
OS type: Linux
Block size=4096 (log=2)
Fragment size=4096 (log=2)
467779584 inodes, 935544823 blocks
46777241 blocks (5.00%) reserved for the super user
First data block=0
Maximum filesystem blocks=4294967296
28551 block groups
32768 blocks per group, 32768 fragments per group
16384 inodes per group
Superblock backups stored on blocks: 
        32768, 98304, 163840, 229376, 294912, 819200, 884736, 1605632, 2654208, 
        4096000, 7962624, 11239424, 20480000, 23887872, 71663616, 78675968, 
        102400000, 214990848, 512000000, 550731776, 644972544

Writing inode tables: done                            
Creating journal (32768 blocks): done
Writing superblocks and filesystem accounting information: done

This filesystem will be automatically checked every 25 mounts or
180 days, whichever comes first.  Use tune2fs -c or -i to override.

# mount /dev/sdb1 /data1

# cat /etc/fstab
/dev/sdb1            /data1          ext3            defaults        0 0 # add this line

#df -h
Filesystem            Size  Used Avail Use% Mounted on
/dev/sda2              95G   15G   76G  16% /
/dev/sda1             247M   42M  193M  18% /boot
/dev/sda3             9.9G  534M  8.9G   6% /tmp
/dev/sda5             9.9G  1.2G  8.2G  13% /home
tmpfs                  95G  336K   95G   1% /dev/shm
/dev/sdb1             3.5T  197M  3.3T   1% /data1
```