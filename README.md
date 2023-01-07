<h1>Active Directory Home Lab</h1>


<h2>Intro</h2>
I have been interested in Microsoft's Active Direct service for sometime. Just a few days ago, I found myself on Youtube watching a 30 minute tutorial by Andy Malone on it's workings (great video by the way. You can check it out via: https://www.youtube.com/watch?v=85-bp7XxWDQ. Since then, I decided I would look into setting up a lab on my own personal computer and test out a few features. I learned a good deal in the process and had some hands on experiencing configuring DHCP Scope and seeing it work as the client computer recieved an IP address from the DC which was a huge plus. Let's get into it! 
<br />


<h2>Languages and Utilities Used</h2>

- <b>PowerShell</b>
- <b>VirtualBox</b>

<h2>Environments Used </h2>

- <b>Windows 10</b> (64-bit)
- <b>Windows Server 2019</b>

<h2>Program walk-through:</h2>

- Step 1: Install VirutalBox. VirtualBox can be installed via [Download](https://www.oracle.com/virtualization/technologies/vm/downloads/virtualbox-downloads.html). Be sure to install the exension pack as well.

- Step 2: Download Windows server 2019 ISO file as well as the Windows 10 ISO file. Both wil take a bit time to download. Take note of the location of both files if they do not default to the computer's Download folder. 
  [Server 2019](https://www.microsoft.com/en-us/evalcenter/download-windows-server-2019)
  [Windows 10](https://www.microsoft.com/en-us/software-download/windows10)
  
- Step 3: Open VirtualBox and click "New" to create a new Virtual Machine (VM). Name as you like but select the Type and Version as shown in below image. I recommend setting the RAM to 2048 MB for better performance but you may keep the default memory size if you are unsure. Click Next < Create < Next < Next < Create (use recommended hard disk size) to create the VM instance.
  ![image](https://user-images.githubusercontent.com/121698544/210188488-81c91803-3028-4c84-8e8d-4a61e33917aa.png)
  
- Step 4: Click Settings in Virtual Box. In settings, go to Advanced within the General tab and set Shared Clipboard and Drag'n'Drop options to Bidirectional to allow copy/paste between your host system and the Virtual Machine. Also select the Network tab and enable Nework Adapter for Adapters 1 and 2. For Adapter 1 select 'NAT' and for Adapater 2 'Internal Network'. This will allow internet connectivity and connectivity between devices in the domain.
![image](https://user-images.githubusercontent.com/121698544/210188941-82b081db-9c5a-40f3-8992-877c7fb061c2.png)
![Recording 2023-01-05 at 20 44 16](https://user-images.githubusercontent.com/121698544/210919095-b0d03244-a62f-4bab-8426-30559e8b8095.gif)


- Step 5: Click the Storage option. Click the Adds Optical Drive option. If the ISO file that was downloaded is not listed, click the Add Disk Image to find and open the file. I have already added the file to my VM instance so it is already selected within the image.
 ![image](https://user-images.githubusercontent.com/121698544/210189019-e6a3ed40-b026-4458-88bb-f11f0ec41ee6.png)
 ![image](https://user-images.githubusercontent.com/121698544/210189049-310bc5c8-f927-46d2-9180-40a4f5674c91.png)
 
- Step 6: Click the Server 2019 VM and click Start. Proceed through installation. Create a username and password for login. For the Operating System selection, select "Windows Server 2019 Evaluation Desktop Experience" and select Custom install for the type of installation. Installation will take a few minutes.
 ![Win2019serverinstall](https://user-images.githubusercontent.com/121698544/210189133-489af2a1-3d8f-4283-af73-80be32339abb.png)

- Step 7: Since CTRL + ALT + Delete will actually toggle your host device's option, you will need to use the Input < Keyboard option within VirtualBox itself to toggle the VM's option.
![Win2019unlock](https://user-images.githubusercontent.com/121698544/210697752-cf56a4fd-b50d-47d1-82a5-5f21c3f0228b.png)

-  Step 8: Once logged, open Network settings and Change Adapter options. Renaming them is the next step as it will be important later on. To tell which ethernet connection is connected to the internet and which is the internal network, Right-Click each < Status < Details. If the IPv4 address begins with "169" this is an APIPA address meaning this connection does not have internet access thus it is the internal network. Rename both connections to differentiate one as internet and one as internal.
![Win2019servernetworks](https://user-images.githubusercontent.com/121698544/210922263-54002d46-b233-468e-a801-621470e624e4.png)

- Step 9: Next, Right-Click the internal network again and select Properties. Select the Internet Protocol 4 (TCP/IP) option then Properties. Without going too much into IP addressing, addresses from 172.16.0.0 to 172.31.255.255 are considered private IP addresses meaning that they are non internet facing and used for internal networks. In this case, I used IP address 172.16.0.1 and subnet mask of 255.255.255.0. Skip default address and enter the loopback address of 127.0.0.1 for the DNS server option because the server itself is it's own DNS.
![IP addressing](https://user-images.githubusercontent.com/121698544/210924475-28cb26f7-af94-4a15-8d79-51462610c2fb.gif)

- Step 10: Time to install AD Domain Services. Use the Add Roles and Features as such below to install. I already have it installed.
![Install AD DS](https://user-images.githubusercontent.com/121698544/210926065-b63d68ec-40e3-48cb-91f2-a07168d7eaa9.gif)

- Step 11: Next, we will need to promote the server to a DC. Click the Notifications icon at the upper right hand corner of the Server Manager (flag) and select 'Promote this Server to a Domain Controller'. Click Add new forest and name the domain. For ex. Mine is called myfirstdomain.com. Proceed and enter a password. Click the Next buttons to finish the process. The server will restart after. Login will now show the domain name/admin name. 

- Step 12: Next, we will proceed in creating our first OU (organizational unit) and object(user) using Active Directory Users and Computer. After adding the new user as a member of the Admin group, log out of the admin profile and login using the user's credentials that was created to test.
![Creating user](https://user-images.githubusercontent.com/121698544/210932127-d5bd3110-da52-4627-b9a5-346b811949cc.gif)

![adding to admin group](https://user-images.githubusercontent.com/121698544/210932820-5381833e-c237-4b4c-9263-6af7bdcfb00d.gif)


- Step 13: Next, installing Remote Access feature which is actually setting up routing to allow the client to access the internet through the DC but with a connection similar to a Virtual Private Network. Click Add roles and features and click Next until you get to the Server Roles screen. Select Remote Access. Click Next until you get to Role Services. Select Routing < Add Features and then click proceed to finish installation.

- Step 14: Click Tools < Routing and Access. Right-Click the DC (local) option then Configure and Enable Routing and Remote Access. After the congifuration wizard screen opens, click Next, select the NAT option. If the 2 connections does not show up after, close the wizard and try again. If they appear, select the internet facing connection (we see why differentiating is important here) and proceed through the remaining steps.

![image](https://user-images.githubusercontent.com/121698544/210935112-c9925686-977a-4f96-876a-bd84621e1ee9.png)

- Step 15: Return to Add roles and features and this time select DHCP Server within Server Roles and continue through installation. The DHCP server is what will provide the windows 10 client with an IP address to access the internet once it joins the domain.

- Step 16: Return to Tools and select DHCP. Click the domain which should show the IPv4 and IPv6 DHCP server options. Right-Click the IPv4 option and select New Scope. Name the scope as you would like and proceed. I set the Start IP address to 172.16.0.100 and the End IP address to 172.16.0.200 so that any client that joins the domain will be assigned an IP address within that range. We will see this happen when the Windows 10 client joins the domain. Set the subnet mask to 255.255.255.0. On the Lease Duration page, set it to any number of days. This is the amount of time the client device will utilize the IP address received. Proceed through installation confirming 'Yes' to configure DHCP options until you arrive at the Router page. On the Router page, add 172.16.0.1 as the default gatway and be sure to click Add. After, Right-Click the domain and select Authorize then Right-Click again and select Refresh to update the DHCP servers. 
![Win2019IPranges](https://user-images.githubusercontent.com/121698544/211154360-dfa9f2a5-b9f6-4861-b171-0ab099ef8b16.png)
![Win2019IPranges-2](https://user-images.githubusercontent.com/121698544/211154398-c11e1584-bbd1-4ea2-a42d-6b416c89a543.png)

- Step 17: The next step involves creating fake users and adding them them to AD. Youtuber Jason Madakor has created a nice powershell script and user.txt file which simplifies this process. His file with both the script and .txt file can be downloaded via https://github.com/joshmadakor1/AD_PS/archive/refs/heads/master.zip but this requires turning off a security feature for Internet Explorer within Server Manager to allow the download. In Server Manager, click Configure this local server then click the ON switch next to IE Enhanced Security Configuration. After, open Internet Explorer copy-paste the link to download the file. Open the file to extract.
![CreateUserscript](https://user-images.githubusercontent.com/121698544/211156679-085fa3e7-1b9b-458c-81fc-26df62773e3a.gif)

- Step 18: Time to open Powershell to run the script. On the Desktop, click Start < Select < Windows PowerShell < Right-click Windows PowerShell ISE < More < Run as Adminstrator. Alternatively, the search function can be used as well to find it. In Powershell, click Open < locate and click 1_CREATE_USERS file < Open. To run the script, we first have to authorize Powershell to run as it will throw a security error. In the command line type "Set-ExecutionPolicy Unrestricted" < Enter on keyboard. Click 'Yes to all' when confirmation prompt appears. After, run the script using the run button in Powershell (green play button). Powrshell should show users being created designed by first initial, last name like image below. If you return to Server Manager < Tools < Users and Computers we can now see users were created.
![Powershell](https://user-images.githubusercontent.com/121698544/211157337-3e9012e2-c71f-49e8-bb51-1f5838c82538.gif)
![Win2019usercreation](https://user-images.githubusercontent.com/121698544/211157371-6721b4f9-45c4-48f7-86b4-70a51ce0d9ed.png)

- Step 19: Now to add Windows client. In VirtualBox, click New and name  as needed. Select Windows for the type if not selected and Windows 64-bit. If your computer is not high in memory, I recommend setting memory size to 2048 MB. Proceed through the installation. Set settings as such below. Be sure to add the ISO image. I have done so below.
![Win10settings](https://user-images.githubusercontent.com/121698544/211157980-8b88f1fe-169b-45fd-9e6c-df60f7c3fd4e.gif)






<br />
<br />
