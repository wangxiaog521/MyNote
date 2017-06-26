## mac添加锁屏快捷键

* 通过Automator新建一个服务，并选取左侧的屏幕保护程序，选择“服务“收到 -> 没有输入
* 确认在finder的服务中可以看到新建的服务
* 打开系统便好设置 -> 键盘，为新建的服务添加快捷键


## 快捷键差异
| 操作 | mac | dell |
| --- | --- | --- |
| 复制 | command+c | win+c |
| 切换输入法 | ctr | ctr |
| 切换界面 | command+tab | wins+tab |
| sublime: home&end | command+-> | wins+-> |
| iterm2: home&end | fn+-> | Home键 |
| iterm2切换 | command+` | wins+` |

## 创建VPN
* 在/etc/ppp目录下新建options文件：
```
sudo vim /etc/ppp/options
plugin L2TP.ppp
l2tpnoipsec
```
* 连接VPN
* 添加路由规则
```
sudo route -n delete -net 192.168.60.33 -netmask 255.255.255.255 192.168.2.17
sudo route -n add -net 192.168.60.33 -netmask 255.255.255.255 192.168.2.17

```
