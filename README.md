<p align="center">
<img src="https://i.imgur.com/Ua7udoS.png" alt="Traffic Examination"/>
</p>

<h1>Network Security Groups (NSGs) and Inspecting Traffic Between Azure Virtual Machines</h1>
In this tutorial, we observe various network traffic to and from Azure Virtual Machines with Wireshark as well as experiment with Network Security Groups. <br />


<h2>Video Demonstration</h2>

- ### [YouTube: Azure Virtual Machines, Wireshark, and Network Security Groups](https://www.youtube.com)

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

- Step 1: Remote desktop into vm
- Step 2: Download Wireshark
- Step 3: Install and Launch App 
- Step 4:  Filter to a specific protocol
- Step 5: monitor packets

<h2>Actions and Observations</h2>

<p>
<img width="874" height="774" alt="image" src="https://github.com/user-attachments/assets/57a395eb-3ba4-444b-ba17-a48362f22c10" />


</p>
<p>
Remote desktop(RDP) is a mechanism used to connect to our VM using our physical computer. After the connection is good and we are in, we would want to download Wireshark protocol analyzer. After launching Wireshark, we can see a flood of traffic displayed. In order to see a specific protocol, we would have to filter down to a specific protocol.
</p>
<br />

<p>
<img width="889" height="889" alt="image" src="https://github.com/user-attachments/assets/ec4ebcc0-6659-44f4-9011-934ed1fbbbe1" />

</p>
<p>
To filter down to analyze the ICMP traffic, we will need to.

  - Get the private IP of vm
  - Open PowerShell
  - Use PING to initiate the ICMP traffic
</p>
<br />

<p>
<img width="1115" height="902" alt="image" src="https://github.com/user-attachments/assets/4ce8e65a-884b-48fc-9ebe-adc302b4edf4" />

<h2>Creating a Network security groups</h2>

</p>
<p>
A network security group contains a set of rules used to block any incoming or outgoing traffic.
  Here are the steps to create this in Azure

  - Click on any VM
  - Go to the network
  - Network settings
  - locate NSG
  - settings under nsg
  - inbound security rules
  - Filter out ICMPV4 and set priority 
   
</p>
<br />


<p>
<img width="1173" height="959" alt="image" src="https://github.com/user-attachments/assets/05f34cc8-f9f9-41cd-8dbe-60e07c61646f" />

</p>
<p>
After configuring the Network security group, we could see that the traffic has been suspended
  Try using the Ping, and you will get a timeout. We also disabled the security group and resumed traffic immediately 
</p>
<br />

<h2>SSH protocol TCP port 22</h2>

</p>
<p>
It is a secure shell that is used to connect to remote machines. Below, we can observe the screenshot. 
  We can see that we have securely connected to our Linux machine and also set up the filter in Wireshark.
  and observe
</p>
<br />


<p>
<img width="1331" height="598" alt="image" src="https://github.com/user-attachments/assets/13c7a9f1-e351-42d3-9871-42473c3a1e85" />


<h2>DHCP traffic UDP port 67 and 68 </h2>

</p>
<p>
DHCP (Dynamic Host Configuration Protocol) is a mechanism that assigns an IP address to different machines, and it uses UDP ports 67 and 68.
  When DHCP is in action, which can be triggered by using 'IPconfig /renew, there are behind-the-scenes processes to take note of; these are 

  - Broadcast
  - Offer
  - Request
  - Acknowledge

    
</p>
<br />

<p>
<img width="1164" height="617" alt="image" src="https://github.com/user-attachments/assets/2b55229c-6b9b-427c-8186-b4d8a27eb0d4" />

</p>
<br />

</p>
<p>
Ran into some issues when running the ipconfig \renew. As seen below, I was only seeing the request.
  
  - HOW TO SOLVE

  - 1: Open Notepad
  - 2: Insert ipconfig \release, ipconfig \renew
  - 3: save file is C drive
  - 4: Back to the PowerShell shell and run the text file
<p>
</p>
<br />

<p>
<img width="437" height="423" alt="image" src="https://github.com/user-attachments/assets/f2ef4d26-b478-4e66-ae7f-7c262371da4b" />


</p>
<br />

<p>
<img width="615" height="627" alt="image" src="https://github.com/user-attachments/assets/b31a5df7-2242-4e4a-ac00-2a7f8013d7f1" />


