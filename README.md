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

- Step 1: Create our Resources
- Step 2: Observe ICMP Traffic
- Step 3: Observe DNS Traffic
- Step 4: Observe RDP Traffic


<h2>Actions and Observations</h2>
<p>

Create our Resources: 
  
1.
   I created a Resource Group to organize my Azure resources. I then set up a Windows 10 Virtual Machine (VM), linking it to the previously made Resource Group. While configuring the VM, I allowed it to create a new Virtual Network (Vnet) and Subnet for seamless connectivity. 

<p>
<img src="https://imgur.com/Hbzr8Db.png" height="50%" width="50%" alt="Disk Sanitization Steps"/>
<img src="https://imgur.com/IUTPpff.png" height="50%" width="50%" alt="Disk Sanitization Steps"/> 
</p>


2.
     I established a Linux (Ubuntu) VM, ensuring it was associated with the existing Resource Group and Vnet. Finally, I checked my Virtual Network within Network Watcher to monitor its performance.
<img src="https://imgur.com/qeVFJWS.png" height="60%" width="60%" alt="Disk Sanitization Steps"/>

</p>
<br />

<p>

3. 
  I connected to my Windows 10 Virtual Machine (VM) using Remote Desktop. Within the VM, I installed Wireshark and filtered for ICMP traffic. 

<img src="https://imgur.com/x8pAZN7.png" height="50%" width="50%" alt="Disk Sanitization Steps"/> 
<img src="https://imgur.com/UISp1Ar.png" height="50%" width="50%" alt="Disk Sanitization Steps"/> 
<img src="https://imgur.com/MqkhwaG.png" height="50%" width="50%" alt="Disk Sanitization Steps"/> 

4. 
  Then, I retrieved the private IP address of the Ubuntu VM and attempted to ping it from within the Windows 10 VM, observing the ping requests and replies in Wireshark. Next, I pinged a public website from the Windows 10 VM and monitored the traffic in Wireshark.

<img src="https://imgur.com/T40IrjV.png" height="50%" width="50%" alt="Disk Sanitization Steps"/> 
<img src="https://imgur.com/dOI4D8B.png" height="50%" width="50%" alt="Disk Sanitization Steps"/> 
<img src="https://imgur.com/4xiusQ6.png" height="50%" width="50%" alt="Disk Sanitization Steps"/> 


5. 
  After that, I initiated a perpetual/non-stop ping from the Windows 10 VM to the Ubuntu VM. Following this, I disabled incoming (inbound) ICMP traffic in the Network Security Group of the Ubuntu VM. I then observed the ICMP traffic in Wireshark and the command line Ping activity from the Windows 10 VM.

<img src="https://imgur.com/vdBfUif.png" height="50%" width="50%" alt="Disk Sanitization Steps"/> 
<img src="https://imgur.com/gwQbmqf.png" height="50%" width="50%" alt="Disk Sanitization Steps"/> 
<img src="https://imgur.com/h8FEui9.png" height="50%" width="50%" alt="Disk Sanitization Steps"/> 


6. 
  Subsequently, I re-enabled ICMP traffic for the Network Security Group of the Ubuntu VM and observed the ICMP traffic in Wireshark and the command line Ping activity, which started working again. Finally, I stopped the ping activity.

<img src="https://imgur.com/a3qssKx.png" height="60%" width="60%" alt="Disk Sanitization Steps"/> 

<br />


7.
  In the next step, I filtered for DNS traffic in Wireshark. From my Windows 10 VM's command line, I used nslookup to query the IP addresses of google.com and disney.com. While performing these lookups, I observed the DNS traffic being displayed in Wireshark.

<img src="https://imgur.com/yvBEZWD.png" height="70%" width="70%" alt="Disk Sanitization Steps"/> 



8.  
  Returning to Wireshark, I filtered for RDP (Remote Desktop Protocol) traffic exclusively using the filter "tcp.port == 3389". Upon observation, I noticed the immediate non-stop spam of traffic. This continuous stream of traffic occurs because the RDP protocol facilitates a live stream from one computer to another, allowing constant transmission of data between the devices. Unlike other protocols where traffic is triggered by specific activities, RDP maintains a constant flow of data to ensure real-time communication between the client and server machines.

<img src="https://imgur.com/3mgpiFv.png" height="70%" width="70%" alt="Disk Sanitization Steps"/> 


<br />
