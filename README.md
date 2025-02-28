# configure-ad
<p align="center">
<img src="https://i.imgur.com/pU5A58S.png" alt="Microsoft Active Directory Logo"/>
</p>

<h1>On-premises Active Directory Deployed in the Cloud (Azure)</h1>
This tutorial outlines the implementation of on-premises Active Directory within Azure Virtual Machines.<br />


<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- Active Directory Domain Services
- PowerShell

<h2>Operating Systems Used </h2>

- Windows Server 2022
- Windows 10 (21H2)


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
From here click on ipconfig1 and under private ip address settings set the allocation from Dynamic to Static. This way the private IP address will not change and will stay the same making it far easier to log into the domain every time.
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
<img src="https://i.imgur.com/bTs96U5.png" height="200%" width="200%" alt="Disk Sanitization Steps"/>
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
<img src="https://i.imgur.com/MsQsLVy.png" height="200%" width="200%" alt="Disk Sanitization Steps"/>
</p>
<p>
Now go into the DNS servers tab and click on the custom option, from here just paste the private IP address of DC-1 and click save.
</p>
<br />

<p>
<img src="https://i.imgur.com/ZJDbMoX.png" height="200%" width="200%" alt="Disk Sanitization Steps"/>
</p>
<p>
Now go back to the Virtual Machines menu and click on Client-1's box and hit restart, this is to make sure that the new settings are applied. 
</p>
<br />

<p>
<img src="https://i.imgur.com/PcSfIS6.png" height="200%" width="200%" alt="Disk Sanitization Steps"/>
</p>
<p>
Now log into Client-1's virtual machine and open up powershell, from there your going to want to copy DC-1's private ip address and ping it inside of powershell. Type in ping (DC-1's private IP adderss) and the following should pop up
</p>
<br />

<p>
<img src="https://i.imgur.com/mvs0RON.png" height="150%" width="150%" alt="Disk Sanitization Steps"/>
</p>
<p>
Now type in the following "ipconfig /all" and the following sequence should occur. If you check the DNS Servers section it should be the same as Dc-1's private ip address. 
  Congratulations you have now connected Client-1 to DC-1's Server! Now onto the next step.
</p>
<br />

<p>
<img src="https://i.imgur.com/AsLC4Ff.png" height="200%" width="200%" alt="Disk Sanitization Steps"/>
</p>
<p>
Now log back into DC-1 and within the server manager screen click on "Add roles and features" go down to server roles and activate "Active Directory Domain Services"
</p>
<br />

<p>
<img src="https://i.imgur.com/KDTPFjB.png" height="200%" width="200%" alt="Disk Sanitization Steps"/>
</p>
<p>
Continue clicking next until you see the following box, make sure to check the box and hit install.
</p>
<br />

<p>
<img src="https://i.imgur.com/msbztfl.png" height="200%" width="200%" alt="Disk Sanitization Steps"/>
</p>
<p>
Within server manager click on the flag on the right right hand corner, click on "Promote this server to a domain controller"
</p>
<br />

<p>
<img src="https://i.imgur.com/BrqRG3n.png" height="200%" width="200%" alt="Disk Sanitization Steps"/>
</p>
<p>
The following window should pop up. Fill in the "Add a new forest" box and make the root domain name "mydomain.com"
</p>
<br />

<p>
<img src="https://i.imgur.com/vnBLxeB.png" height="200%" width="200%" alt="Disk Sanitization Steps"/>
</p>
<p>
On the next tab chances are you may never need this but for the sake of this lesson put a memorable password and hit next.
</p>
<br />

<p>
<img src="https://i.imgur.com/Hh8QFaI.png" height="200%" width="200%" alt="Disk Sanitization Steps"/>
</p>
<p>
Now continue to this tab and hit install, your virtual macine should automatically reset itself.
</p>
<br />

<p>
<img src="https://i.imgur.com/ubfo4HD.png" height="200%" width="200%" alt="Disk Sanitization Steps"/>
</p>
<p>
When attempting to log back into DC-1 be sure to put "mydomain.com\" then YOUR username this is important since we are now logging back into DC-1 now that it is an offical Domain. 
</p>
<br />

<p>
<img src="https://i.imgur.com/Ocndybo.png" height="200%" width="200%" alt="Disk Sanitization Steps"/>
</p>
<p>
Now that you've logged in click on the windows start button, expand "Windows Administrative Tools" and click on "Active Directory Users and Computers"
</p>
<br />

<p>
<img src="https://i.imgur.com/pLD3TlD.png" height="200%" width="200%" alt="Disk Sanitization Steps"/>
</p>
<p>
You should be met with the following screen from here right click "mydomain.com" Go to New, go down and click "Orginizational Unit"
</p>
<br />

<p>
<img src="https://i.imgur.com/C9V14e2.png" height="150%" width="150%" alt="Disk Sanitization Steps"/>
</p>
<p>
Name the orginizational unit "_EMPLOYEES" Do NOT mess this part up be sure that your spelling is correct and that you are not missing the underscore.
</p>
<br />

<p>
<img src="https://i.imgur.com/PHVfP6i.png" height="200%" width="200%" alt="Disk Sanitization Steps"/>
</p>
<p>
Create another orginizational unit following the same process, name this one "_ADMINS" Same rules apply as the last one make sure there are no mistakes when doing this.
</p>
<br />

<p>
<img src="https://i.imgur.com/n22cgMw.png" height="200%" width="200%" alt="Disk Sanitization Steps"/>
</p>
<p>
Now we want to create a user within the AD. Go to _ADMINS and right click the empty folder, go to new and click on user. 
</p>
<br />

<p>
<img src="https://i.imgur.com/DmL19jj.png" height="200%" width="200%" alt="Disk Sanitization Steps"/>
</p>
<p>
Fill out the following information, feel free to name your user whatever you'd like but make sure there is an underscore afrer their first name, make sure that "admin" is following the underscore. This will be used to log into the Domain as this user.
</p>
<br />

<p>
<img src="https://i.imgur.com/VJXK3Nv.png" height="200%" width="200%" alt="Disk Sanitization Steps"/>
</p>
<p>
Now that you created the account in order to fully make this account a true admin you have to add the created account into the domain's security group. Right click the account and go to properties.
</p>
<br />

<p>
<img src="https://i.imgur.com/u7RFe49.png" height="200%" width="200%" alt="Disk Sanitization Steps"/>
</p>
<p>
This window should pop up from here go to "Member Of" and click on "Add" type in "Domain Admins" and hit "Check Names" it should add the account as a Domain Admin be sure to hit "Apply" and "Ok"
</p>
<br />
<p>
<img src="https://i.imgur.com/eNkMtfl.png" height="200%" width="200%" alt="Disk Sanitization Steps"/>
</p>
<p>
Now log out of the account and log back in as the previously created account. After you've logged into DC-1, log in to Client-1 aswell.
</p>
<br />

<p>
<img src="https://i.imgur.com/qkFJfkE.png" height="200%" width="200%" alt="Disk Sanitization Steps"/>
</p>
<p>
From Client-1's machine right click the windows start button and go to system, from there click on Rename this PC.
</p>
<br />

<p>
<img src="https://i.imgur.com/BlPaGNe.png" height="200%" width="200%" alt="Disk Sanitization Steps"/>
</p>
<p>
The first window that pops up should be system propereties, click change. Now from the ComputerName/DomainChanges window click on Domain and type in mydomain.com and hit OK.
</p>
<br />

<p>
<img src="https://i.imgur.com/Eb8VRcK.png" height="200%" width="200%" alt="Disk Sanitization Steps"/>
</p>
<p>
Now type in the information from the previously created account, it should look something like this.
</p>
<br />

<p>
<img src="https://i.imgur.com/9MYIeNg.png" height="200%" width="200%" alt="Disk Sanitization Steps"/>
</p>
<p>
If you've done everything correctly this window should appear. Your virtual machine should be asking to restart, after this restart Client-1 should be a member of the domain.
</p>
<br />

<p>
<img src="https://i.imgur.com/9EFKZ8V.png" height="200%" width="200%" alt="Disk Sanitization Steps"/>
</p>
<p>
Now from DC-1 (NOT CLIENT-1) go to start and head over to "Active Directory Users and Computers"
</p>
<br />

<p>
<img src="https://i.imgur.com/084Mq6I.png" height="200%" width="200%" alt="Disk Sanitization Steps"/>
</p>
<p>
Now to confirm that Client-1 was successfully added to the domain, expand "mydomain.com" and click on "computers" you should see client-1 within the computers tab.
</p>
<br />

<p>
<img src="https://i.imgur.com/ki5UHVZ.png" height="200%" width="200%" alt="Disk Sanitization Steps"/>
</p>
<p>
Log into Client-1 as the previously created admin account and right-click windows start, from there click system and go to remote desktop on the window that pops up.
</p>
<br />

<p>
<img src="https://i.imgur.com/lcW3uRY.png" height="200%" width="200%" alt="Disk Sanitization Steps"/>
</p>
<p>
From the Remote Desktop window click on "Select users that can remotely access this PC. Click Add on the window that opens up.
</p>
<br />

<p>
<img src="https://i.imgur.com/zxpWz02.png" height="200%" width="200%" alt="Disk Sanitization Steps"/>
</p>
<p>
Type in Domain Users in the box and click check names, from there click ok and log into DC-1 as the previously created admin account.
</p>
<br />

<p>
<img src="https://i.imgur.com/uv32i1e.png" height="200%" width="200%" alt="Disk Sanitization Steps"/>
</p>
<p>
From within DC-1 go to the windows search bar and type "Powershell ISE" right-click and run powershell as an administrator.
</p>
<br />

<p>
<img src="https://i.imgur.com/Z2i3FlM.png" height="200%" width="200%" alt="Disk Sanitization Steps"/>
</p>
<p>
Go to this link https://github.com/joshmadakor1/AD_PS/blob/master/Generate-Names-Create-Users.ps1 . Hit the copy button and head back over to DC-1 and paste the copied content into powershell. All the following code does is essentially creates a whole lot of different random made up user accounts within the active directory so we can get a better understanding of how it should look inside an actual Domain.
</p>
<br />

<p>
<img src="https://i.imgur.com/4FEGY6V.png" height="200%" width="200%" alt="Disk Sanitization Steps"/>
</p>
<p>
Once the script has been pasted into the engine hit run script and it should make 1000 random accounts for you to work with. Each and every single created user will automatically have the password: Password1
</p>
<br />

<p>
<img src="https://i.imgur.com/tM4Vk94.png" height="200%" width="200%" alt="Disk Sanitization Steps"/>
</p>
<p>
Now head over to Active Directory Users and Computers, got to mydomain.com and click on the _EMPLOYEES folder, you should see all of the created users within the folder. From here we can log into one of these users using Client-1's virtual machine so go ahead and choose a random name and log into Client-1. Remember all of the passwords for these accounts are automatically: Password1 .
</p>
<br />

<p>
<img src="https://i.imgur.com/oAkRO05.png" height="200%" width="200%" alt="Disk Sanitization Steps"/>
</p>
<p>
The sign in process should look something like this. After successfully logging in feel free to sign out.
</p>
<br />

<p>
<img src="https://i.imgur.com/p5QOImb.png" height="200%" width="200%" alt="Disk Sanitization Steps"/>
</p>
<p>
Now go back into DC-1's VM and right click the windows start button and hit run. From there type in "gpmc.msc" and hit run. This should take you to the Group Policy Management page. Within mydomain.com your going to want to look for Group Policy Object and right-click it.
</p>
<br />

<p>
<img src="https://i.imgur.com/RrL7aVr.png" height="200%" width="200%" alt="Disk Sanitization Steps"/>
</p>
<p>
Click on New and name this policy Account Lockout Policy, this is to ensure that whenever a user fails their log in attempts more then a set number out times their account will be locked out.
</p>
<br />

<p>
<img src="https://i.imgur.com/pp79yjq.png" height="200%" width="200%" alt="Disk Sanitization Steps"/>
</p>
<p>
Click on the new created policy and go to settings from there scroll down and right-click Computer Configuration and click on edit.
</p>
<br />

<p>
<img src="https://i.imgur.com/JElqU65.png" height="200%" width="200%" alt="Disk Sanitization Steps"/>
</p>
<p>
From here your going to want to open the following folders, Computer Configuration > Policies > Windows Settings > Security Settings > Account Policies > Account Lockout Policy. 
</p>
<br />

<p>
<img src="https://i.imgur.com/E2C1lRP.png" height="200%" width="200%" alt="Disk Sanitization Steps"/>
</p>
<p>
Double click Account Lockout Duration and check the "Define this policy setting" box and set the timer to 5 minutes.
</p>
<br />

<p>
<img src="https://i.imgur.com/vKUp16z.png" height="200%" width="200%" alt="Disk Sanitization Steps"/>
</p>
<p>
Next double click on Account lockout threshold and set it to 3 invalid logon attempts.
</p>
<br />

<p>
<img src="https://i.imgur.com/jDnb68U.png" height="200%" width="200%" alt="Disk Sanitization Steps"/>
</p>
<p>
Now the last policy we're going to edit is the "Reset account lockout counter after" policy, double click and set the timer to 10 minutes. This policy makes sure that after you failed one logon attempt the set 10 minute timer will begin, if you attempt to logon before those 10 minutes are up the it would count as your 2nd logon attempt, if you attempt to logon after those 10 minutes then the counter would reset and it would only count as your first logon attempt.
</p>
<br />

<p>
<img src="https://i.imgur.com/EdywgFV.png" height="200%" width="200%" alt="Disk Sanitization Steps"/>
</p>
<p>
Now go back into the Group Policy Management section and right-click mydomain.com and click on "Link an Existing GPO"
</p>
<br />

<p>
<img src="https://i.imgur.com/CzQL5cg.png" height="200%" width="200%" alt="Disk Sanitization Steps"/>
</p>
<p>
This window should appear your going to want to click on the previoously created policy "Account Lockout Policy" and hit OK. The policy should automatically update overtime. We have officially configured Active Directory and the polcies that come with it Congratulations!
</p>
<br />

