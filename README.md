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
Create a new resource group. Feel free to name it whatever you like, just make sure to remember which resource group you're using for Active Directory.
</p>
<br />

<p>
<img src="https://i.imgur.com/Q4spr7m.png" height="200%" width="200%" alt="Disk Sanitization Steps"/>
</p>
<p>
Create a virtual network and ensure that it is within the previously created resource group.
</p>
<br />

<p>
<img src="https://i.imgur.com/L8dwMyZ.png" height="200%" width="200%" alt="Disk Sanitization Steps"/>
</p>
<p>
Create two virtual machines named DC-1 (Domain Controller) and Client-1. Make sure that they're both assigned to the previously created resource group and virtual network. DC-1's image should be Windows Server 2022, and Client-1's image should be Windows 10 Pro.
</p>
<br />

<p>
<img src="https://i.imgur.com/RzkdslB.png" height="200%" width="200%" alt="Disk Sanitization Steps"/>
</p>
<p>
DC-1's private IP address is subject to change at the moment because its IP address settings are set to Dynamic, not Static. To change this, go into DC-1's network settings and click on dc-1449_z1.
</p>
<br />

<p>
<img src="https://i.imgur.com/I45Dnvl.png" height="200%" width="200%" alt="Disk Sanitization Steps"/>
</p>
<p>
From here, click on Ipconfig1, and under Private IP address settings, change the allocation from Dynamic to Static. This way, the private IP address will not change and will stay the same, making it far easier to log in to the domain every time.
</p>
<br />

<p>
<img src="https://i.imgur.com/RkaTr1t.png" height="200%" width="200%" alt="Disk Sanitization Steps"/>
</p>
<p>
Start DC-1's virtual machine, and you should see this screen inside the Server Manager application. If you do not see this screen, you may have missed a step or made a mistake.
</p>
<br />

<p>
<img src="https://i.imgur.com/yYSeRiR.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Right-click on the Windows Start button, then click on Run. A window should pop up. Type in the command wf.msc.
</p>
<br />

<p>
<img src="https://i.imgur.com/bTs96U5.png" height="200%" width="200%" alt="Disk Sanitization Steps"/>
</p>
<p>
You should see this screen, then click on Windows Defender Firewall Properties.
</p>
<br />

<p>
<img src="https://i.imgur.com/jB9a4wW.png" height="200%" width="200%" alt="Disk Sanitization Steps"/>
</p>
<p>
This window should open up. You're going to want to go through each of the following tabs: Domain Profile, Private Profile, and Public Profile. Make sure the firewall state is set to Off, then click Apply.
</p>
<br />

<p>
<img src="https://i.imgur.com/phzUxmE.png" height="200%" width="200%" alt="Disk Sanitization Steps"/>
</p>
<p>
Now, go back into Azure and copy DC-1's private IP address. We'll need this to change Client-1's connection to DC-1 instead of Azure itself.
</p>
<br />

<p>
<img src="https://i.imgur.com/zXzdRjC.png" height="200%" width="200%" alt="Disk Sanitization Steps"/>
</p>
<p>
Go to Client-1's network settings and click on the network interface client01393_z1.
</p>
<br />

<p>
<img src="https://i.imgur.com/MsQsLVy.png" height="200%" width="200%" alt="Disk Sanitization Steps"/>
</p>
<p>
Now, go to the DNS Servers tab and click the Custom option. From here, paste the private IP address of DC-1 and click Save.
</p>
<br />

<p>
<img src="https://i.imgur.com/ZJDbMoX.png" height="200%" width="200%" alt="Disk Sanitization Steps"/>
</p>
<p>
Now, go back to the Virtual Machines menu, click on Client-1's entry, and click Restart to ensure that the new settings are applied. 
</p>
<br />

<p>
<img src="https://i.imgur.com/PcSfIS6.png" height="200%" width="200%" alt="Disk Sanitization Steps"/>
</p>
<p>
Now, log into Client-1's virtual machine and open up PowerShell. From there, you're going to want to copy DC-1's private IP address and ping it in PowerShell. Type in ping [DC-1's private IP address], and the following output should appear.
</p>
<br />

<p>
<img src="https://i.imgur.com/mvs0RON.png" height="150%" width="150%" alt="Disk Sanitization Steps"/>
</p>
<p>
Now, type in the following: ipconfig /all, and the following output should appear. If you check the DNS Servers section, it should match DC-1's private IP address. Congratulations, you have now connected Client-1 to DC-1's server! Now, onto the next step.
</p>
<br />

<p>
<img src="https://i.imgur.com/AsLC4Ff.png" height="200%" width="200%" alt="Disk Sanitization Steps"/>
</p>
<p>
Now, log back into DC-1, and in the Server Manager window, click on Add roles and features. Scroll down to Server Roles and select Active Directory Domain Services.
</p>
<br />

<p>
<img src="https://i.imgur.com/KDTPFjB.png" height="200%" width="200%" alt="Disk Sanitization Steps"/>
</p>
<p>
Continue clicking Next until you reach the following screen. Make sure to check the box and click Install.
</p>
<br />

<p>
<img src="https://i.imgur.com/msbztfl.png" height="200%" width="200%" alt="Disk Sanitization Steps"/>
</p>
<p>
Within Server Manager, click the flag in the right-hand corner, then click Promote this server to a domain controller.
</p>
<br />

<p>
<img src="https://i.imgur.com/BrqRG3n.png" height="200%" width="200%" alt="Disk Sanitization Steps"/>
</p>
<p>
The following window should appear. Select the 'Add a new forest' option and set the root domain name to 'mydomain.com'
</p>
<br />

<p>
<img src="https://i.imgur.com/vnBLxeB.png" height="200%" width="200%" alt="Disk Sanitization Steps"/>
</p>
<p>
On the next tab, you may never need this, but for the sake of this lesson, enter a memorable password and click Next.
</p>
<br />

<p>
<img src="https://i.imgur.com/Hh8QFaI.png" height="200%" width="200%" alt="Disk Sanitization Steps"/>
</p>
<p>
Now, continue to the next tab and click Install. Your virtual machine should automatically restart."
Let me know if you'd like any further refinements!
</p>
<br />

<p>
<img src="https://i.imgur.com/ubfo4HD.png" height="200%" width="200%" alt="Disk Sanitization Steps"/>
</p>
<p>
When attempting to log back into DC-1, make sure to enter 'mydomain.com' followed by your username. This is important because we are now logging into DC-1, which is now an official domain. 
</p>
<br />

<p>
<img src="https://i.imgur.com/Ocndybo.png" height="200%" width="200%" alt="Disk Sanitization Steps"/>
</p>
<p>
Now that you're logged in, click the Windows Start button, expand Windows Administrative Tools, and click Active Directory Users and Computers.
</p>
<br />

<p>
<img src="https://i.imgur.com/pLD3TlD.png" height="200%" width="200%" alt="Disk Sanitization Steps"/>
</p>
<p>
You should see the following screen. From here, right-click on 'mydomain.com,' go to New, then select Organizational Unit.
</p>
<br />

<p>
<img src="https://i.imgur.com/C9V14e2.png" height="150%" width="150%" alt="Disk Sanitization Steps"/>
</p>
<p>
Name the organizational unit '_EMPLOYEES.' Do not mess this up—make sure the spelling is correct and that the underscore is included.
</p>
<br />

<p>
<img src="https://i.imgur.com/PHVfP6i.png" height="200%" width="200%" alt="Disk Sanitization Steps"/>
</p>
<p>
Create another organizational unit using the same process and name it '_ADMINS.' The same rules apply as before—make sure there are no mistakes when naming it.
</p>
<br />

<p>
<img src="https://i.imgur.com/n22cgMw.png" height="200%" width="200%" alt="Disk Sanitization Steps"/>
</p>
<p>
Go to '_ADMINS' and right-click the empty folder. Go to New, then click User.
</p>
<br />

<p>
<img src="https://i.imgur.com/DmL19jj.png" height="200%" width="200%" alt="Disk Sanitization Steps"/>
</p>
<p>
Fill out the following fields. Feel free to name your user whatever you'd like, but make sure there is an underscore after their first name and that 'admin' follows the underscore. This username will be used to log into the domain as this user.
</p>
<br />

<p>
<img src="https://i.imgur.com/VJXK3Nv.png" height="200%" width="200%" alt="Disk Sanitization Steps"/>
</p>
<p>
Now that you've created the account, to fully grant this account admin privileges, you need to add the account to the domain's security group. Right-click the account and select Properties.
</p>
<br />

<p>
<img src="https://i.imgur.com/u7RFe49.png" height="200%" width="200%" alt="Disk Sanitization Steps"/>
</p>
<p>
This window should appear. From here, go to the Member Of tab and click Add. Type in 'Domain Admins' and click Check Names. It should add the account as a Domain Admin. Be sure to click Apply and then OK.
</p>
<br />

<p>
<img src="https://i.imgur.com/eNkMtfl.png" height="200%" width="200%" alt="Disk Sanitization Steps"/>
</p>
<p>
Now, log out of the current account and log back in using the previously created account. After logging into DC-1, log in to Client-1 as well.
</p>
<br />

<p>
<img src="https://i.imgur.com/qkFJfkE.png" height="200%" width="200%" alt="Disk Sanitization Steps"/>
</p>
<p>
On Client-1's machine, right-click the Windows Start button and select System. From there, click Rename this PC.
</p>
<br />

<p>
<img src="https://i.imgur.com/BlPaGNe.png" height="200%" width="200%" alt="Disk Sanitization Steps"/>
</p>
<p>
The first window that pops up should be System Properties. Click Change. Now, in the Computer Name/Domain Changes window, click on Domain, type in 'mydomain.com', and click OK.
</p>
<br />

<p>
<img src="https://i.imgur.com/Eb8VRcK.png" height="200%" width="200%" alt="Disk Sanitization Steps"/>
</p>
<p>
Now, enter the information from the previously created account. It should look something like the following.
</p>
<br />

<p>
<img src="https://i.imgur.com/9MYIeNg.png" height="200%" width="200%" alt="Disk Sanitization Steps"/>
</p>
<p>
If you've done everything correctly, this window should appear. Your virtual machine should prompt you to restart. After the restart, Client-1 should be a member of the domain.
</p>
<br />

<p>
<img src="https://i.imgur.com/9EFKZ8V.png" height="200%" width="200%" alt="Disk Sanitization Steps"/>
</p>
<p>
Now, from DC-1 (NOT CLIENT-1), click Start and open Active Directory Users and Computers.
</p>
<br />

<p>
<img src="https://i.imgur.com/084Mq6I.png" height="200%" width="200%" alt="Disk Sanitization Steps"/>
</p>
<p>
Now, to confirm that Client-1 was successfully added to the domain, expand mydomain.com and click on Computers. You should see Client-1 listed under the Computers tab.
</p>
<br />

<p>
<img src="https://i.imgur.com/ki5UHVZ.png" height="200%" width="200%" alt="Disk Sanitization Steps"/>
</p>
<p>
Log into Client-1 using the previously created admin account, then right-click the Windows Start button. From there, click System, then go to Remote Desktop in the window that appears.
</p>
<br />

<p>
<img src="https://i.imgur.com/lcW3uRY.png" height="200%" width="200%" alt="Disk Sanitization Steps"/>
</p>
<p>
In the Remote Desktop window, click on Select users that can remotely access this PC. Click Add in the window that opens.
</p>
<br />

<p>
<img src="https://i.imgur.com/zxpWz02.png" height="200%" width="200%" alt="Disk Sanitization Steps"/>
</p>
<p>
Type in 'Domain Users' in the box and click Check Names. From there, click OK and log into DC-1 using the previously created admin account.
</p>
<br />

<p>
<img src="https://i.imgur.com/uv32i1e.png" height="200%" width="200%" alt="Disk Sanitization Steps"/>
</p>
<p>
From within DC-1, go to the Windows search bar and type 'PowerShell ISE.' Right-click and select Run as Administrator.
</p>
<br />

<p>
<img src="https://i.imgur.com/Z2i3FlM.png" height="200%" width="200%" alt="Disk Sanitization Steps"/>
</p>
<p>
Go to the following link: https://github.com/joshmadakor1/AD_PS/blob/master/Generate-Names-Create-Users.ps1. Click the copy button, head back to DC-1, and paste the copied content into PowerShell. All this code does is create a large number of randomly generated user accounts within Active Directory, allowing us to better understand how it should look in an actual domain.
</p>
<br />

<p>
<img src="https://i.imgur.com/4FEGY6V.png" height="200%" width="200%" alt="Disk Sanitization Steps"/>
</p>
<p>
Once the script has been pasted into the engine, click Run Script. It should then create 1,000 random accounts for you to work with. Each created user will automatically have the password: Password1.
</p>
<br />

<p>
<img src="https://i.imgur.com/tM4Vk94.png" height="200%" width="200%" alt="Disk Sanitization Steps"/>
</p>
<p>
Now, head over to Active Directory Users and Computers, go to mydomain.com, and click on the _EMPLOYEES folder. You should see all the created users within the folder. From here, you can log into one of these users using Client-1's virtual machine. Go ahead and choose a random name and log into Client-1. Remember, all of the passwords for these accounts are automatically Password1
</p>
<br />

<p>
<img src="https://i.imgur.com/oAkRO05.png" height="200%" width="200%" alt="Disk Sanitization Steps"/>
</p>
<p>
The sign-in process should look something like this. After successfully logging in, feel free to sign out.
</p>
<br />

<p>
<img src="https://i.imgur.com/p5QOImb.png" height="200%" width="200%" alt="Disk Sanitization Steps"/>
</p>
<p>
Now, go back into DC-1's VM, right-click the Windows Start button, and click Run. From there, type in 'gpmc.msc' and click Run. This should take you to the Group Policy Management Console. Within mydomain.com, you will want to look for Group Policy Objects and right-click it.
</p>
<br />

<p>
<img src="https://i.imgur.com/RrL7aVr.png" height="200%" width="200%" alt="Disk Sanitization Steps"/>
</p>
<p>
Click on New and name the policy 'Account Lockout Policy.' This policy ensures that whenever a user exceeds a set number of failed login attempts, their account will be locked out.
</p>
<br />

<p>
<img src="https://i.imgur.com/pp79yjq.png" height="200%" width="200%" alt="Disk Sanitization Steps"/>
</p>
<p>
Click on the newly created policy and go to Settings. From there, scroll down, right-click Computer Configuration, and click on Edit.
</p>
<br />

<p>
<img src="https://i.imgur.com/JElqU65.png" height="200%" width="200%" alt="Disk Sanitization Steps"/>
</p>
<p>
From here, you're going to want to open the following folders: Computer Configuration > Policies > Windows Settings > Security Settings > Account Policies > Account Lockout Policy.
</p>
<br />

<p>
<img src="https://i.imgur.com/E2C1lRP.png" height="200%" width="200%" alt="Disk Sanitization Steps"/>
</p>
<p>
Double-click Account Lockout Duration and check the Define this policy setting box, then set the duration to 5 minutes.
</p>
<br />

<p>
<img src="https://i.imgur.com/vKUp16z.png" height="200%" width="200%" alt="Disk Sanitization Steps"/>
</p>
<p>
Next, double-click on Account Lockout Threshold and set it to 3 invalid login attempts.
</p>
<br />

<p>
<img src="https://i.imgur.com/jDnb68U.png" height="200%" width="200%" alt="Disk Sanitization Steps"/>
</p>
<p>
The last policy we're going to edit is the Reset account lockout counter after policy. Double-click on it and set the timer to 10 minutes. This policy ensures that after you fail one login attempt, the 10-minute timer begins. If you attempt to log in before those 10 minutes are up, it will count as your second login attempt. If you attempt to log in after those 10 minutes, the counter will reset, and it will count as your first login attempt.
</p>
<br />

<p>
<img src="https://i.imgur.com/EdywgFV.png" height="200%" width="200%" alt="Disk Sanitization Steps"/>
</p>
<p>
Now, go back to the Group Policy Management Console. Right-click mydomain.com and click on Link an Existing GPO.
</p>
<br />

<p>
<img src="https://i.imgur.com/CzQL5cg.png" height="200%" width="200%" alt="Disk Sanitization Steps"/>
</p>
<p>
This window should appear. You're going to want to click on the previously created policy Account Lockout Policy and click OK. The policy should automatically update over time. We have officially configured Active Directory and the policies that come with it. Congratulations!
</p>
<br />

