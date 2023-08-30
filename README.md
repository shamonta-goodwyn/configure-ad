<p align="center">
<img src="https://i.imgur.com/Cxfcc5D.png" alt="Microsoft azure logo"/>
</p>

<h1>Configuring Active Directory within Azure VMs</h1>
This tutorial outlines the prerequisites, installation, and configuration of Active Directory.<br />

<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- Internet Information Services (IIS)

<h2>Operating Systems Used </h2>

- Windows 10</b> (21H2)
- Windows Data Center Server</b> (21H2)

<h2>List of Prerequisites</h2>

- Azure Account
- Microsoft Remote Desktop (Mac)

<h2>Installation Steps</h2>

<p>
<img src="https://i.imgur.com/LJ3kkWf.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
<img src="https://i.imgur.com/P9CFKaQ.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
<img src="https://i.imgur.com/WfAcA4c.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
<img src="https://i.imgur.com/VXCDHZj.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
<img src="https://i.imgur.com/PjRicuj.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
<img src="https://i.imgur.com/6k0wQFQ.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
<img src="https://i.imgur.com/rd88DbL.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
You want to start by downloading Microsoft Remote Desktop if you're on Mac. Next you will make an Azure account. Once that is made you will make a resource group. In the group will be 2 VMs. The first VM will be the Directory Controller which you will pick the Windows Data Center VM. The second VM you make will be a regular Windows 10 VM. Make sure they are in the same region and give the Windows 10 VM the same network that the WIndows Data Center VM have. To make this simple I will refer to them as DC-1 and VM1.
</p>
<br />

<p>
<img src="https://i.imgur.com/HFwkszG.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
<img src="https://i.imgur.com/sk7EdDS.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
You will then need to set DC-1 NIC to static from dynamic so the IP address doesn't change. You do this by going to the network tab on the DC-1 VM. You then select the NIC. IP Configurations will be next selection. Right after select ipconfig and chnge the setting to static. You will need to perform an ICMP or ping from VM to DC-1. To do this you must make a open port in the firewall for them to talk to each other. You must use the IP address in MRD (microsoft remote desktop) to do this in the terminal. input the command ping -t and the private IP address of DC-1.
</p>
<br />

<p>
<img src="https://i.imgur.com/qvjy4Z7.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
<img src="https://i.imgur.com/Tv79iox.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
<img src="https://i.imgur.com/Sc1vtX4.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
<img src="https://i.imgur.com/XNZgPnY.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
<img src="https://i.imgur.com/Jg3ktpy.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
<img src="https://i.imgur.com/ubPBOKN.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
<img src="https://i.imgur.com/ItaroRc.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
<img src="https://i.imgur.com/VCN78rC.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
<img src="https://i.imgur.com/ndF5HMM.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Next you will use Remote Desktop to view or VM GUI. Once in you will need to open the firewall on DC-1 to allow ICMP from VM1. DO this by go to DC-1 start menu and then type in WF.MSC and then selecting inbound rules. Filter by protocol and enable the two selected rules as shown in picture. You will then go to VM1 terminal and ping the private IP address of DC-1. If you get packets back then you know it is good. 
</p>
<br />

<p>
<img src="https://i.imgur.com/LrNXW1k.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
<img src="https://i.imgur.com/vUGfr2d.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
<img src="https://i.imgur.com/ub0T83Q.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
<img src="https://i.imgur.com/hC7MVW5.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
<img src="https://i.imgur.com/kH8Jd9A.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
<img src="https://i.imgur.com/TnPpznL.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
<img src="https://i.imgur.com/UFfndeP.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
We are going to now install active directory on DC-1 and promote it to domain controller. In server manager click add features and services. click next through and select active directory and services and keep clicking next and install. Click the flag up in the right hand corner and click promote this server to domain controller. You will then select add new forest and put in anything for the domain. I simply put mydomain.com. you will then click next through everything and install and it should restart your VM automactically. You will then log in after the DC-1 is done restarting with the mydomain.com\*** that you created. so if you used labuser in the beginning as the user of the VM then it will be that mydomain.com\labuser. You now have created a domain controller. 
</p>
<br />
