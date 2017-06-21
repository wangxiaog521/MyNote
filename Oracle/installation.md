## Oracle 10.2.0.5安装部署
### 1. 必要的包检查：
* 32位Linux中
```shell
rpm -q binutils compat-db compat-libstdc++-33 glibc glibc-devel glibc-headers gcc gcc-c++ libXp libstdc++ cpp make libaio ksh elfutils-libelf sysstat libaio libaio-devel setarch --qf '%{name}.%{arch}\n'|sort
```
* 64位Linux中
```shell
rpm -q binutils compat-db compat-libstdc++-33 glibc glibc-devel glibc-headers gcc gcc-c++ libXp libstdc++ cpp make libaio ksh elfutils-libelf sysstat libaio libaio-devel setarch --qf '%{name}.%{arch}\n'|sort
# 检查32包
rpm -qa glibc-devel libXp libXt libXtst | egrep 'i386|i686'
```	
### 2. 配置本地yum安装必要的包
#### 2.1. 根据镜像文件挂载镜像盘
```shell
mount -t iso9660 -o loop CentOS-6.5-x86_64-bin-DVD1.iso   /mnt/server/
```
#### 2.2. 配置本地yum源,baseurl必须为repodata/repomd.xml的上一级
```shell
cd /etc/yum.repos.d/
mkdir backup
mv * backup
vi shawn.repo
[shawn]
name=shawn
baseurl=file:///media/
enable=1
gpgcheck=0
```
#### 2.3. 安装上一步中显示未安装的软件
```shell
yum install gcc
yum list available
yum whatprovides gcc
```

### 3. 设置内核参数
* kernel.shmmax  
用于定义单个共享内存段的最大值，shmmax 设置应该足够大，能在一个共享内存段下容纳下整个的SGA
Oralce 建议 SHMMAX > SGA(SGA_MAX_SIZE)，这样在任何时候都不会有甚至轻微的性能下降的隐患。
通过ipca -sa查看oracle使用多少个内存段，一个为正常

* kernel.shmall  
该参数是控制共享内存页数。该参数大小为物理内存除以pagesize;
查看os系统页的大小
```shell
#getconf PAGESIZE
4096
```
这里显示的pagesize 是4k，假设一个共享内存段的最大大小是16G，那么需要共享内存页数是 16GB/4KB=16777216KB/4KB=4194304 （页），也就是64Bit 系统下16GB 物理内存，设置 kernel.shmall = 4194304 才符合要求，几乎是原来设置2097152的两倍。

* kernel.shmmni 参数  
该参数是共享内存段的最大数量。shmmni 缺省值 4096 ，一般肯定是够用了。

* fs.file-max 参数  
fs.file-max为512 乘以 processes。
如2000个process，则file-max=512*2000=1024000
		
* 参数生效  
```shell
/sbin/sysctl -p
```
### 4. 配置用户资源
```shell
vi /etc/security/limits.conf
# added for oracle
oracle              soft    nproc   65536
oracle              hard    nproc   65536
oracle              soft    nofile  65536
oracle              hard    nofile  65536
```

### 5. 创建用户
```shell
# /usr/sbin/groupadd oinstall
# /usr/sbin/groupadd dba
# /usr/sbin/useradd -g oinstall -G dba oracle
# mkdir -p /app/oracle
# chown -R oracle:oinstall /app/oracle
# passwd oracle
```

### 6. 修改操作系统版本
```shell
vi /etc/redhat-release
注释掉 #Red Hat Enterprise Linux Server release 5.2 (Tikanga)
添加 redhat-4
```
	
### 7. 修改oracle用户环境变量
```shell
export ORACLE_BASE=/app/oracle
export ORACLE_HOME=$ORACLE_BASE/10.2.0/db
export ORACLE_SID=SMHISDB
export ORACLE_TERM=xterm
export ORACLE_OWNER=oracle
export NLS_LANG=AMERICAN_AMERICA.ZHS16GBK
export LD_LIBRARY_PATH=$ORACLE_HOME/lib:$LD_LIBRARY_PATH; 
export PATH=$ORACLE_HOME/bin:$PATH
alias alert='tail -200f /app/oracle/admin/rac/bdump/alert_rac1.log'
```

### 8. 以oracle用户登录并开始安装
* 安装序列

| file | release |
| --- | --- |
| 10201_database_linux_x86_64.cpio | 安装10.2.0.1.0 在el6上即使安装386包安装会报错(ins_ctx.mk等)，可忽略继续安装 |
| p6810189_10204_Linux-x86-64.zip | 升级到10.2.0.4.0 |
| p8202632_10205_Linux-x86-64.zip | 升级到10.2.0.5.0 |
| p6880880_102000_Linux-x86-64.zip | 升级opatch到10.2.5.1 上一步升级完成opatch只到10.2.0.4.9 |
| p16619894_10205_Linux-x86-64.zip | 打10.2.0.5.0 PSU patch包 |


#### Chap 1. install oracle software
1. upload file and unzip file cpio -idmv < 10201_database_linux_x86_64.cpio

2. create file oraInst.loc in /etc  
```shell
#cat > /etc/oraInst.loc
inventory_loc=/app/oracle/oraInventory
inst_group=oinstall
#chown oracle:oinstall oraInst.loc 
#chmod 664 oraInst.loc 
```

3. create file in /home/oracle/enterprise01.rsp
```shell
$ cat enterprise01.rsp
RESPONSEFILE_VERSION=2.2.1.0.0
FROM_LOCATION="../stage/products.xml"
ORACLE_HOME="/app/oracle/10.2.0/db/"
ORACLE_HOME_NAME="OraDb10g_home1"
TOPLEVEL_COMPONENT={"oracle.server","10.2.0.1.0"}  
DEINSTALL_LIST={"oracle.server","10.2.0.1.0"}
SHOW_SPLASH_SCREEN=false
SHOW_WELCOME_PAGE=false
SHOW_COMPONENT_LOCATIONS_PAGE=false
SHOW_CUSTOM_TREE_PAGE=false
SHOW_SUMMARY_PAGE=false
SHOW_INSTALL_PROGRESS_PAGE=false
SHOW_REQUIRED_CONFIG_TOOL_PAGE=false
SHOW_CONFIG_TOOL_PAGE=false
SHOW_RELEASE_NOTES=false
SHOW_ROOTSH_CONFIRMATION=false
SHOW_END_SESSION_PAGE=false
SHOW_EXIT_CONFIRMATION=false
NEXT_SESSION=false
NEXT_SESSION_ON_FAIL=false
SHOW_DEINSTALL_CONFIRMATION=false
SHOW_DEINSTALL_PROGRESS=false
ACCEPT_LICENSE_AGREEMENT=true
COMPONENT_LANGUAGES={"en"}
CLUSTER_NODES=
INSTALL_TYPE="EE"
s_nameForDBAGrp=dba
s_nameForOPERGrp=dba
b_oneClick=false
SHOW_DATABASE_CONFIGURATION_PAGE=false
b_createStarterDB=false
DECLINE_SECURITY_UPDATES=true # 忽约oracle的metalink账号验证
```

4. add the follow lines in profile
```shell
# added
export ORACLE_BASE=/home/oracle/app/oracle
export ORACLE_HOME=/home/oracle/app/oracle/10.2.0/db
export ORACLE_SID=SHUMIDEV1
export NLS_LANG=AMERICAN_AMERICA.ZHS16GBK
export PATH=$PATH:$ORACLE_HOME/bin
```

5. check file in /etc/redhat-release
```shell
$ cat  /etc/redhat-release
redhat 4
```

6. install using below command
```shell
$ ./runInstaller -silent -ignoreSysPrereqs -responseFile /home/oracle/enterprise01.rsp
```

#### Chap 2: create database using rman duplicate
1. make sure both side have the same version, if not, upgrade it  
```shell
unzip file p6810189_10204_Linux-x86-64.zip  
cd disk1  
./runInstaller -silent -ignoreSysPrereqs -responseFile /home/oracle/enterprise01.rsp
```

2. create pfile from spfile in source database and scp it to target database

3. modify initSID.ora for bellow parameters
```
SID.__db_cache_size=2231369728
SID.__java_pool_size=50331648
SID.__large_pool_size=16777216
SID.__shared_pool_size=771751936
SID.__streams_pool_size=33554432
*.db_name='SID'
```

4. create spfile from pfile in target database and startup nomount the database

5. create rman backup in target database
```sql
RMAN> backup format '/home/oracle/backup/df_t%t_s%s_p%p' database;
RMAN> sql 'alter system archive log current';
RMAN> backup format '/home/oracle/backup/al_t%t_s%s_p%p' archivelog all delete input;
```

6. scp backup files to target database and duplicate it
```shell
$ rman target sys/"oracle"@orcl auxiliary sys/oracle

Recovery Manager: Release 10.2.0.4.0 - Production on Tue Dec 22 00:05:19 2015

Copyright (c) 1982, 2007, Oracle.  All rights reserved.

connected to target database: ORCL (DBID=1425719928)
connected to auxiliary database: SID (not mounted)

RMAN> duplicate target database to SID nofilenamecheck
logfile group 1 ('/home/oracle/oradata/orcl/redo1_1.log','/home/oracle/oradata/orcl/redo1_2.log') size 512M,
group 2 ('/home/oracle/oradata/orcl/redo2_1.log','/home/oracle/oradata/orcl/redo2_2.log') size2> 3>  512M,
group 3 ('/home/oracle/oradata/orcl/redo3_1.log','/home/oracle/oradata/orcl/redo3_2.log') size 512M;4> 
```

### 9. dbca创建实例
	
### 10. 启动监听
	
