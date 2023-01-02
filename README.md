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
  
- Step 4: Click Settings in Virtual Box. In settings, go to Advanced within the General tab and set Shared Clipboard and Drag'n'Drop options to Bidirectional to allow copy/paste between your host system and the Virtual Machine.
![image](https://user-images.githubusercontent.com/121698544/210188941-82b081db-9c5a-40f3-8992-877c7fb061c2.png)

- Step 5: Click the Storage option. Click the Adds Optical Drive option. If the ISO file that was downloaded is not listed, click the Add Disk Image to find and open the file. I have already added the file to my VM instance so it is already selected within the image.
 ![image](https://user-images.githubusercontent.com/121698544/210189019-e6a3ed40-b026-4458-88bb-f11f0ec41ee6.png)
 ![image](https://user-images.githubusercontent.com/121698544/210189049-310bc5c8-f927-46d2-9180-40a4f5674c91.png)
 
- Step 6: Click the Server 2019 VM and click Start.
 ![Win2019serverinstall](https://user-images.githubusercontent.com/121698544/210189133-489af2a1-3d8f-4283-af73-80be32339abb.png)



<br />
<br />
