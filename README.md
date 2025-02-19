# configure-ad
<p align="center">
<img src="https://i.imgur.com/pU5A58S.png" alt="Microsoft Active Directory Logo"/>
</p>

<h1>On-premises Active Directory Deployed in the Cloud (Azure)</h1>
This tutorial outlines the implementation of on-premises Active Directory within Azure Virtual Machines.<br />


<h2>Video Demonstration</h2>

- ### [YouTube: How to Deploy on-premises Active Directory within Azure Compute](https://www.youtube.com)

<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- Active Directory Domain Services
- PowerShell

<h2>Operating Systems Used </h2>

- Windows Server 2022
- Windows 10 (21H2)

<h2>High-Level Deployment and Configuration Steps</h2>

- Step 1
- Step 2
- Step 3
- Step 4

<img src="https://i.imgur.com/3KoaBl6.png" height="150%" width="150%" alt="Disk Sanitization Steps"/>
</p>
<p>
Create a new resource group. Feel free to name it whatever just make sure to remember which resource group your using for Active Directory.
</p>
<br />

<p>
<img src="https://i.imgur.com/Q4spr7m.png" height="200%" width="200%" alt="Disk Sanitization Steps"/>
</p>
<p>
Create a Virtual Network, make sure that it's within the previously created resource group.
</p>
<br />

<p>
<img src="https://i.imgur.com/L8dwMyZ.png" height="200%" width="200%" alt="Disk Sanitization Steps"/>
</p>
<p>
Create two Virtual Machines named DC-1 (Domain Controller) and Client-1, make sure that they're both assigned to the previously created Resource Group and Vitrual Network. DC-1's image should be under Windows Server 2022 and Client-1's image should be under Windows 10 Pro.
</p>
<br />

<p>
<img src="https://i.imgur.com/RzkdslB.png" height="200%" width="200%" alt="Disk Sanitization Steps"/>
</p>
<p>
Dc-1's Private ip address is subject to change at the moment because it's IP address settings is set to Dynamic not Static, To change this go into Dc-1's network settings and click on dc-1449_z1.
</p>
<br />

<p>
<img src="https://i.imgur.com/I45Dnvl.png" height="200%" width="200%" alt="Disk Sanitization Steps"/>
</p>
<p>
From here click on ipconfig1 and under private ip address settings set the allocation from Dynamic to Static. This way the priavte IP address will not change and will stay the same making it far easier to log into the domain every time.
</p>
<br />

<p>
<img src="https://i.imgur.com/RkaTr1t.png" height="200%" width="200%" alt="Disk Sanitization Steps"/>
</p>
<p>
Load up DC-1's Virtual Machine and you should be met with this screen inside the application Server Manager, if you are not met with this screen chances are you missed a step or did something wrong.
</p>
<br />

<p>
<img src="https://i.imgur.com/yYSeRiR.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Right Click on the windows start button from there click on run, a window should pop up type in the command wf.msc
</p>
<br />

<p>
<img src="https://i.imgur.com/bTs96U5.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
You should be met with this screen, click on Windows Defender Firewall Properties.
</p>
<br />

<p>
<img src="https://i.imgur.com/jB9a4wW.png" height="200%" width="200%" alt="Disk Sanitization Steps"/>
</p>
<p>
This window should open up. Your going to want to go through each of the following tabs Domain Profile, Private Profile, and Public Profile. Make sure the firewall state is set to off for each tab and apply.
</p>
<br />

<p>
<img src="https://i.imgur.com/phzUxmE.png" height="200%" width="200%" alt="Disk Sanitization Steps"/>
</p>
<p>
Now go back into azure and copy DC-1's private IP address. We're going to need this to change Client-1's connection to DC-1 instead of azure itself.
</p>
<br />

<p>
<img src="https://i.imgur.com/zXzdRjC.png" height="200%" width="200%" alt="Disk Sanitization Steps"/>
</p>
<p>
Go into Client-1's network settings and click on the network interface/client01393_z1. 
</p>
<br />

<p>
<img src="https://i.imgur.com/MsQsLVy.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Now go into the DNS servers tab and click on the custom option, from here just paste the private IP address of DC-1 and click save.
</p>
<br />

<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur.
</p>
<br />

<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur.
</p>
<br />

<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur.
</p>
<br />
