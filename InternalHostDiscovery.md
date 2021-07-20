Initial Host Discovery
---------------------------------------------------------------
sudo nmap -oA live_hosts --stats-every 60s --log-errors --traceroute --reason --randomize-hosts -v -R -PE -PP -PM -PO -PU -PY 80,23,443,21,22,25,3389,110,445,139,53,135,3306,8080,1723,111,995,93,5900,1025,587,8888,199,1720,465,548,113,81,6001,10000,514,5060,179,1026,2000,8443,8000,32768,554,26,1433,49152,2001,515,8008,49154,1027,5666,646 -PA  80,23,443,21,22,25,3389,110,445,139,53,135,3306,8080,1723,111,995,93,5900,1025,587,8888,199,1720,465,548,113,81,6001,10000,514,5060,179,1026,2000,8443,8000,32768,554,26,1433,49152,2001,515,8008,49154,1027,5666,646 -sS -sV -p 21,22,23,25,80,443,445,8080,8443 -iL scope.txt


SMB Common Vuln Checks
---------------------------------------------------------------
--script smb-vuln-ms17-010
--script smb-vuln-ms08-067


Additional Host Discovery - Recheck
---------------------------------------------------------------

nmap -sP -PA21,22,25,3389 192.168.2.1/24 
sudo nmap -sP -PS22,3389 192.168.2.1/24 
sudo nmap -sP -PU161 192.168.2.1/24 

Host Discovery of 6 most common ports
---------------------------------------------------------------
sudo nmap -sP -PS21,22,80,139,445,3389


Fast Live host discovery trick (checks only .1 on subnet):
---------------------------------------------------------------
sudo nmap -sn 10.0-255.0-255.1 -PE —min-hostgroup 10000 —min-rate 10000
(Then do normal fast discovery on confirmed subnet)
Discover banners:
    curl -head ip or hostname


NMAP ping sweep:
----------------------------------------------
sudo nmap -sn -iL discovery/ranges.txt -oA discovery/hosts/pingsweep -PE


NMAP quick RMI discovery scan:
-------------------------------------------
nmap -Pn -n -p 22,80,443,3389,2222 -iL discovery/ranges.txt  -oA discovery/hosts/rmisweep —min-hostgroup 256 —min-rate 1280

Cut results from RMI scan to 'Open' ports: cat discovery/hosts/rmisweep.gnmap |grep open | cut -d " " -f2


NMAP common port scan:
--------------------------------------------------------------------------
nmap -Pn -n -p 22,25,53,80,443,445,1433,3306,3389,5800,5900,8080,8443  -iL hosts/targets.txt -oA services/quick-sweep


NMAP Scan all ports:
---------------------------
nmap -Pn -n -iL targets.txt -p 0-65535 -sV -A -O -oA filename -min-rate 50000 min-hostgroup 22


To find out which NMAP .NSE script ran from above:
--------------------------------------------------
cat services/full-sweep.nmap |grep '|_' | cut -d '_' -f2 | cut -d ' ' -f1 | sort -u | grep ':'
for just HTTP targets: cat full-sweep.nmap | grep -i http-title


Common RCE Ports
---------------------------------------------------------------
nmap -oA commonRCE -iL live_hosts.txt -p 1090,1098,1099,4444,11099,47001,47002,10999,7000-7004,8000-8003,9000-9003,9503,7070,7071,45000,45001,8686,9012,50500,4848,11111,4445,4786,5555,5556 --open


Common Web Ports
---------------------------------------------------------------
nmap -p 80,443,8443,8080,8081,8444,8000,8100,8082,8001,8002,8500,8888,9000,8200,9000,8200,8008,8181,8900,8009 -iL live_hosts.txt -oA common_web_ports --open


Using Aquatone to visualize
---------------------------------------------------------------
cat common_web_ports.xml | .\aquatone.exe -nmap -chrome-path "C:\Program Files\Google\Chrome\Application\Chomre.exe" -out C:\Users\Magic\Desktop\aquatone

