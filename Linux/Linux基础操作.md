## Linux添加用户
```shell
id # 显示用户信息，以及已加入的用户组
useradd # 添加一个用户
useradd -u 505 -g 505 -G root log # 添加用户并制定UID，GUID和root用户组

usermod -G root log # log加入root组

groupadd -g 505 log # 添加log用户组
```

## iterm2断开连接
mac下在~/.ssh/config里添加如下：
```shell
ServerAliveInterval 50
```

## 个性化.bash_profile
```shell
export PS1='\n\e[1;37m[\e[m\e[1;32m\u\e[m\e[1;33m@\e[m\e[1;35m\H\e[m \e[4m`pwd`\e[m\e[1;37m]\e[m\e[1;36m\e[m\n\$ '
```