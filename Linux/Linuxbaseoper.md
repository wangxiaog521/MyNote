## Linux添加用户
```shell
id # 显示用户信息，以及已加入的用户组
useradd # 添加一个用户
useradd -u 505 -g 505 -G root log # 添加用户并制定UID，GUID和root用户组

usermod -G root log # log加入root组

groupadd -g 505 log # 添加log用户组
```
