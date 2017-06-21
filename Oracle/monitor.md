## monitor_standby.sh
```shell
#!/bin/bash

. /home/oracle/.bash_profile

LogFile=/home/oracle/shawn/scripts/logs/$(echo ${0##*/} | awk -F'.' '{print $1}')_$(date +'%Y%m%d_%H%M%S').log

unset -f logwrite
function logwrite()
{
	echo "$(date +'%Y-%m-%d %H:%M:%S') [INFO]: $1" >> ${LogFile}
}

logwrite "start monitor standby"
delaysb=$(echo -e "set head off;\nselect round((sysdate-min(checkpoint_time))*24*60) from v\$datafile;"|sqlplus -s sys/oracle@TNS_SB as sysdba|sed 's/[^0-9]//g' | sed '/^$/d')
delaybc=$(echo -e "set head off;\nselect round((sysdate-min(checkpoint_time))*24*60) from v\$datafile;"|sqlplus -s sys/oracle@TNS_BCP as sysdba|sed 's/[^0-9]//g' | sed '/^$/d')
logwrite "${delaysb},${delaybc}"
[[ "$delaysb" =~ ^[0-9]+$ ]] && (( $delaysb < 30 )) && [[ "$delaybc" =~ ^[0-9]+$ ]] && (( $delaybc < 5 )) && \
[[ ! `echo "${delaysb}${delaybc}" | grep "ORA-"` ]] && [[ "$(date +%H%M)" != "2100" ]] || \
{
    ssh root@192.168.1.1 "echo 'INFO:
S${delaysb};B${delaybc}'| mail -s 'S-TM' XXXXXXXXXXX@139.com" >> ${LogFile}
}

logwrite "finish monitor standby"
```
