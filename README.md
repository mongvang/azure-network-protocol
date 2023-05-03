<p align="center">
<img src="https://i.imgur.com/Ua7udoS.png" alt="Traffic Examination"/>
</p>

<h1>Network Security Groups (NSGs) and Inspecting Traffic Between Azure Virtual Machines</h1>
In this tutorial, we observe various network traffic to and from Azure Virtual Machines with Wireshark as well as experiment with Network Security Groups. <br />

<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- Various Command-Line Tools
- Various Network Protocols (SSH, RDH, DNS, HTTP/S, ICMP)
- Wireshark (Protocol Analyzer)

<h2>Operating Systems Used </h2>

- Windows 10 (21H2)
- Ubuntu Server 20.04

<h2>High-Level Steps</h2>

- Create our Resources
- Observe ICMP Traffic
- Observe SSH Traffic
- Observe DHCP Traffic
- Observe DNS Traffic
- Observe RDP Traffic

<h2>Actions and Observations</h2>

<p> 1) Create a Resource Group<br>
Create a Windows 10 Virtual Machine (VM)<br>
While creating the VM, select the previously created Resource Group<br>
While creating the VM, allow it to create a new Virtual Network (Vnet) and Subnet<br>
Create a Linux (Ubuntu) VM<br>
While create the VM, select the previously created Resource Group and Vnet<br>
Observe Your Virtual Network within Network Watcher<br>
</p>
<p>
<img src="https://i.imgur.com/WIYje5W.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<br />

<p> 2) Use Remote Desktop to connect to your Windows 10 Virtual Machine<br>
Within your Windows 10 Virtual Machine, Install Wireshark<br>
Open Wireshark and filter for ICMP traffic only<br>
Retrieve the private IP address of the Ubuntu VM and attempt to ping it from within the Windows 10 VM<br>
Observe ping requests and replies within WireShark<br>
From The Windows 10 VM, open command line or PowerShell and attempt to ping a public website (such as www.google.com) and observe the traffic in WireShark<br>
Initiate a perpetual/non-stop ping from your Windows 10 VM to your Ubuntu VM<br>
-Open the Network Security Group your Ubuntu VM is using and disable incoming (inbound) ICMP traffic<br>
-Back in the Windows 10 VM, observe the ICMP traffic in WireShark and the command line Ping activity<br>
-Re-enable ICMP traffic for the Network Security Group your Ubuntu VM is using<br>
-Back in the Windows 10 VM, observe the ICMP traffic in WireShark and the command line Ping activity (should start working)<br>
-Stop the ping activity
</p>
<p>
<img src="https://i.imgur.com/xig5xVZ.png" height="100%" width="100%" alt="Disk Sanitization Steps"/>
<img src="https://i.imgur.com/vMpCvpU.png" height="100%" width="100%" alt="Disk Sanitization Steps"/>
</p>
<br />

<p> 3) Back in Wireshark, filter for SSH traffic only<br>
From your Windows 10 VM, “SSH into” your Ubuntu Virtual Machine (via its private IP address)<br>
Type commands (username, pwd, etc) into the linux SSH connection and observe SSH traffic spam in WireShark<br>
</p>
<p>
<img src="https://i.imgur.com/LJwIICk.png" height="80%" width="80%" alt="Disk Sanitization Steps"/><br>
Connection Successful to VM2 (Linux)<br>
<img src="https://i.imgur.com/7wsMbI6.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<br />

<p> 4) Back in Wireshark, filter for DHCP traffic only<br>
From your Windows 10 VM, attempt to issue your VM a new IP address from the command line (ipconfig /renew)<br>
Observe the DHCP traffic appearing in WireShark<br>
</p>
<p>
<img src="https://i.imgur.com/vKZlF0b.png" height="80%" width="80%" alt="Disk Sanitization Steps"/><br>
</p>
<br />

<p> 5) Back in Wireshark, filter for DNS traffic only<br>
From your Windows 10 VM within a command line, use nslookup to see what google.com and disney.com’s IP addresses are<br>
Observe the DNS traffic being show in WireShark<br>
</p>
<p>
<img src="https://i.imgur.com/QuF64Jb.png" height="80%" width="80%" alt="Disk Sanitization Steps"/><br>
Traffic coming through Google's IP Address<br>
<img src="https://i.imgur.com/T8Sonyh.png" height="80%" width="80%" alt="Disk Sanitization Steps"/><br>
</p>
<br />

<p> 6) Back in Wireshark, filter for RDP traffic only (tcp.port == 3389)<br>
Observe the immediate non-stop spam of traffic? Why do you think it’s non-stop spamming vs only showing traffic when you do an activity?<br>
</p>
<p>
<img src="https://i.imgur.com/B9F7TQA.png" height="80%" width="80%" alt="Disk Sanitization Steps"/><br>
</p>
Answer: because the RDP (protocol) is constantly showing you a live stream from one computer to another, therefor traffic is always being transmitted<br>
<br />

