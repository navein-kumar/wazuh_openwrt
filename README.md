```
#enable syslog and fowrd to rsylog sever frm openwrit 
# Login ssh to openwrt root shell --> update below cmd fr sending IP (rsyslog server IP )and port number

uci set system.@system[0].log_ip='10.20.0.10'
uci set system.@system[0].log_port='515'
uci set system.@system[0].log_proto='udp'
uci set system.@system[0].log_remote='1'
uci commit system
/etc/init.d/log restart

```
```
#rsyslog recider frm openwrt add confi last end of file -> revier port number --> 515,  and openwrt ip --> 10.20.0.100
#Add at the end:

$ModLoad imudp
$UDPServerRun 515

if $fromhost-ip == '10.20.0.100' then /var/log/openwrt.log
& stop

```
```
#add rules and decoder and below wazuh config 

<localfile>
  <log_format>syslog</log_format>
  <location>/var/log/openwrt.log</location>
</localfile>
```
