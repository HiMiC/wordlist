


## Брутфорс

nmap
```
# словарь nmap
sudo nmap -sU -p 161 --script snmp-brute <IP>

# свой словарь
sudo nmap -sU -p 161 --script snmp-brute  --script-args snmp-brute.communitiesdb=/opt/wordlist/SNMP/community.txt <IP>
```

Брутфорс используя onesixtyone

Версия для Windows https://github.com/InitRoot/onesixtyonewin/

https://github.com/trailofbits/onesixtyone
https://github.com/trailofbits/onesixtyone/releases


```text
git clone https://github.com/trailofbits/onesixtyone.git
cd onesixtyone/
make

./onesixtyone -c /opt/wordlist/SNMP/community.txt  <IP>

./onesixtyone -c /opt/wordlist/SNMP/community.txt  -i hosts.txt -o community_true.log -w 100
```



## Получение информации

Для использования нам понадобятся установка: snmpset snmpwalk snmpbulkwalk
```
apt install snmp snmp-mibs-downloader
```


Nmap NSE Скрипты
```text
ls -1 /usr/share/nmap/scripts/snmp-* 

snmp-brute.nse 
snmp-hh3c-logins.nse 
snmp-info.nse 
snmp-interfaces.nse 
snmp-ios-config.nse 
snmp-netstat.nse 
snmp-процессы.nse 
snmp-sysdescr.nse 
snmp-win32-services.nse 
snmp-win32-shares.nse 
snmp-win32-software.nse 
snmp-win32-users.nse 
```


```text
sudo nmap -sU -p 161 --script snmp-info <IP>

PORT    STATE SERVICE
161/udp open  snmp
| snmp-info: 
|   enterprise: MikroTik
|   engineIDFormat: text
|   engineIDData: 
|   snmpEngineBoots: 0
|_  snmpEngineTime: 0s
```

Получение информации о подключенных интерфейсах (если доступен public)
```
sudo nmap -sU -p 161 --script snmp-interfaces  <IP>


PORT    STATE SERVICE
161/udp open  snmp
| snmp-interfaces: 
|   sfp-sfpplus1
|     MAC address: e4:00:8c:1d:00:47 (Routerboard.com)
|     Type: ethernetCsmacd  Speed: 0 Kbps
|     Status: down
|     Traffic stats: 0.00 Kb sent, 0.00 Kb received
|   sfp1
|     MAC address: e4:00:8c:1d:00:48 (Routerboard.com)
|     Type: ethernetCsmacd  Speed: 1 Gbps
|     Status: up
|     Traffic stats: 1.94 Gb sent, 3.45 Gb received
|   ether1
|     IP address: 178.000.000.000  Netmask: 255.255.255.248
|     MAC address: e4:00:8c:1d:00:49 (Routerboard.com)
|     Type: ethernetCsmacd  Speed: 1 Gbps
|     Status: up
|     Traffic stats: 3.60 Gb sent, 144.18 Mb received
```

Извлекаем данные SNMP с помощью snmpwalk по протоколу v1 или v2c

```text
snmpwalk -v1 -c public <IP> .
snmpwalk -v2c -c public <IP> .

snmpbulkwalk -v1 -c public <IP> .
snmpbulkwalk -v2c -c public <IP> .

snmpwalk -v1 -c private <IP> .
snmpwalk -v2c -c private <IP> .

snmpbulkwalk -v1 -c private <IP> .
snmpbulkwalk -v2c -c private <IP> .
```


Использование snmpenum
```text
git clone https://github.com/ajohnston9/snmpenum.git
cd snmpenum/
perl snmpenum.pl

perl snmpenum.pl <IP>  public linux.txt
perl snmpenum.pl <IP>  public windows.txt
perl snmpenum.pl <IP>  public cisco.txt
```


## Shodan

https://www.shodan.io/search?query=port%3A161

```
port:161
port:161 product:"MikroTik"
port:161 country:"RU"
port:161 country:"KZ"

```