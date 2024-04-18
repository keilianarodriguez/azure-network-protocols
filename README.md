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
- Step 3: Observe SSH Traffic
- Step 4: Observe DHCP Traffic
- Step 5: Observe DNS Traffic
- Step 6: Observe RDP Traffic


<h2>Actions and Observations</h2>

<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>

  Create our Resources: 
  
I created a Resource Group to organize my Azure resources. Next, I set up a Windows 10 Virtual Machine (VM), linking it to the previously made Resource Group. While configuring the VM, I allowed it to create a new Virtual Network (Vnet) and Subnet for seamless connectivity. 

<p>
<img src="https://imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>


Then, I established a Linux (Ubuntu) VM, ensuring it was associated with the existing Resource Group and Vnet. Finally, I checked my Virtual Network within Network Watcher to monitor its performance.

</p>
<br />

<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>

I connected to my Windows 10 Virtual Machine (VM) using Remote Desktop. Within the VM, I installed Wireshark and filtered for ICMP traffic. Then, I retrieved the private IP address of the Ubuntu VM and attempted to ping it from within the Windows 10 VM, observing the ping requests and replies in Wireshark. Next, I pinged a public website from the Windows 10 VM and monitored the traffic in Wireshark.

After that, I initiated a perpetual/non-stop ping from the Windows 10 VM to the Ubuntu VM. Following this, I disabled incoming (inbound) ICMP traffic in the Network Security Group of the Ubuntu VM. I then observed the ICMP traffic in Wireshark and the command line Ping activity from the Windows 10 VM.

Subsequently, I re-enabled ICMP traffic for the Network Security Group of the Ubuntu VM and observed the ICMP traffic in Wireshark and the command line Ping activity, which started working again. Finally, I stopped the ping activity.
</p>
<br />

<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
  
Returning to Wireshark, I filtered for SSH traffic exclusively. Then, from my Windows 10 VM, I initiated an SSH connection to my Ubuntu Virtual Machine using its private IP address. Within the SSH session, I entered commands such as username and password, observing the influx of SSH traffic in Wireshark. To exit the SSH connection, I typed 'exit' and pressed [Enter].
</p>
<p>


Returning to Wireshark, I filtered for DHCP traffic exclusively. Then, from my Windows 10 VM, I attempted to issue my VM a new IP address using the command line (ipconfig /renew), while observing the DHCP traffic appearing in Wireshark.


In the next step, I filtered for DNS traffic in Wireshark. From my Windows 10 VM's command line, I used nslookup to query the IP addresses of google.com and disney.com. While performing these lookups, I observed the DNS traffic being displayed in Wireshark.



Returning to Wireshark, I filtered for RDP (Remote Desktop Protocol) traffic exclusively using the filter "tcp.port == 3389". Upon observation, I noticed the immediate non-stop spam of traffic. This continuous stream of traffic occurs because the RDP protocol facilitates a live stream from one computer to another, allowing constant transmission of data between the devices. Unlike other protocols where traffic is triggered by specific activities, RDP maintains a constant flow of data to ensure real-time communication between the client and server machines.








<br />
