# Active-Directory-Home-Lab
Step by step directions on how to set up a home lab running Active Directory with test users to mimic an office environment. No prior VMware or Active Directory experience required.
# Step 1. Set up and install your VMware (Oracle VirtualBox)
[Click here](https://www.virtualbox.org/) to visit the Oracle VirtualBox official website to begin downloading. Run the executable and follow the installation instructions.
# Step 2. Download Windows Server 2019 ISO and Windows 10 ISO
[Click here](https://www.microsoft.com/en-us/evalcenter/download-windows-server-2019) to download Windows Server 2019 ISO
[Click here](https://www.microsoft.com/en-us/software-download/windows10) to download Windows 10 installation media. Ensure you select "Create installation media (USB flash drive, DVD, or ISO file) for another PC", then choose the "ISO file" option when prompted.
# Step 3. Set up the first virtual machine (Windows Server 2019)
Open Oracle VirtualBox. Click New (CTRL + N). 
Under VM name, call it "DC" for this exercise (domain controller). 
Under "specify virtual hardware", allocate an appriopriate amount of memory and CPU based on how much you have (keep in mind we will be running two virtual machines at the same time). 
Click Finish. 
Click your virtual machine "DC" and go into settings.
Under Network, click Adapter 2, then under Attached to click Internal Network. Finish by clicking OK.
Start "DC"
A pop up asking to select a virtual optical disk file or physical optical drive containing a disk to start should appear. Select the Windows Server 2019 ISO file.
DC should then begin the process of installing Windows Servers 2019.
After installing WIndows Server 2019 and landing on the home screen, open Control Panel -> Network and Internet -> Network Connections.
Right click each Ethernet individually -> Status -> Details. Rename the one with the automatically assigned IPv4 address 169.254.215.39 to Internal Network to distinguish the external NIC with internet access. PIC 1
Set the internal NIC IP and DNS address by right clicking Internal Network -> Properties -> Highlight Internet Protocol Version 4 -> Properties -> Set IP address to 172.16.0.1, Subnet mask to 255.255.255.0, DNS server to 127.0.0.1 (localhost) PIC 2
# Step 4. Create a Domain (AD DS)
Open Server Manager -> Under Configure this local server click add roles and features -> Next until you reach server roles. Select AD DS -> Next until Install and close. PIC 3
Top right of the UI/Screen is a flag and a yellow warning sign. Click to then promote this server to a domain controller.
Add a new forest -> Type mydomain.com then click Next -> Type a generic password for the sake of the experiment then Click Next all the way to Install. Pic 4
Set up RAS/NAT (allows client on the private network to connect to the internet via the domain controller) by going to Server Manager Dashboard -> Add roles and features -> Ensure you select your server -> Next until you reach roles. Tick Remote Access -> Next until you can Tick DirectAccess and VPN (RAS) and Routing -> Next and Install PIC 5
To enable the RAS/NAT, on the Server Manager Dashboard select Tools -> Routing and Remote Access -> Right click your server -> Configure and Enable Routing and Remote Access -> Next, then Select Network address translation (NAT) -> Under Use this puiblic interface to connect to the internet select Ethernet (the network adapter that has internet connection. If it is greyed out, exit out of the setup wizard and right click your server, then refresh) -> Next and Finish. PIC 6
# Step 5. Set up DHCP server on the Domain Controller
Serv
