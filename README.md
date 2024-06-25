# Azure-Point-to-site
Point-to-site VPN connection
1.Create the resource group.

```bash
 Resouce group name:
 Region: 
```
2.Create VNet in resource group.

```bash
1. Basic tab 
 Resource group:
 Virtual network name: 
 Region: (Same as resource group)

2. IP addresses tab
 Edit
 Subnet purpose: default
 Name:
 IPv4 addresses range: 
 Starting address:
 Size:
```

3.Create Gateway Subnet.
```bash
Subnet purpose: Virtual Network Gateway
IPv4 address range:
Starting address:
Size:
```
4.Create virtual network gateway.
```bash
Name:
Region: Same as resource group.
Gateway type: VPN
SKU: VpnGw1
Generation: Generation1
Virtual network: (Select the gatway subnet).
Public IP address: Create one.
Public IP address name:
Enable active-active mode: Disable.
Configure BGP: Disable.
```
- Go to  virtual network gateway.
- on left hand side click "Point-to-site configuration".
- Click configure now.

5.Virtual network gateway | Point-to-site.
```bash
Address pool:(Give the address pool)
Tunnel type:open VPN(SSL) For every OS.
            SSTP for Windows OS.
Authentication type:Azure Certificate.                
```

## create self signed root Certificate and client Certificate.

- [Certificate P2S](https://www.google.com/search?q=Azure+point+to+site+VPN+certificate&oq=Azure+point+to+site+VPN+certificate&gs_lcrp=EgZjaHJvbWUyBggAEEUYOTIGCAEQRRg9MgYIAhAuGEDSAQg3ODA2ajBqMagCALACAA&sourceid=chrome&ie=UTF-8)




- In create the self signed root certifficate. Copy that script 
- Open powershell as a administrator and run that script.(self signed root has  generated).
- To loacte the certificate go to "certmgr.msc".
- on left hand side go to personal > certificates (you'll see P2S root certificate).
- Export the certificate on your pc. (To Export right click All task > Export, Next > Next, select base 64 encoded Next and Export on your pc. Next, finish).
- Deploy the certificete in Azure

```bash
Root certificate
Name:               
Public certificate data:(open the root certificate with notepad,
copy and paste the content except 1st and last line).
Click save.
```
- To create the client certificate Go back to the link.
- In generate the client certificate copy the script.
- Open powershell as a administrator and run that script.(client certificate has generated)
- To loacte the certificate go to "certmgr.msc".
- on left hand side go to personal > certificates (you'll see P2S client certificate).
- Export the certificate in PC. (To Export right click all task > Export, Next > yes,Export the private key Next > Next Select the passwd "mention the passwd" > Next > browse > Save).

Note: The client certificate extension has .pfx


## Deploy the Client certificate in Client laptop.

- Double click on the certificate 
- Current user Next > Next > passwd Next > Next > finish.

## Configure the VPN client

- Download the VPN client from the portal.
- Unzip the downloaded folder.
- Select the suitable installer according to your pc.
- rightclick on it run as administrator > Yes > 
