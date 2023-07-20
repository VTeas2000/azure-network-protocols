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

- Set up resources in Microsoft Azure
- Observe ICMP Traffic
- Observe ICMP Traffic and Configure Network Security Groups
- Observe SSH Traffic
- Observe DNS Traffic
- Observe RDP Traffic

<h3>Set up resources in Microsoft Azure</h3>
<p>
Create a Windows 10 virtual machine within a new resource group with any credentials. Keep them in mind.
<img src="https://github.com/VTeas2000/azure-network-protocols/assets/60052902/41da9734-6363-470c-889f-15b70348773e" height="80%" width="80%" alt="Windows VM"/>
<br>Create an Ubuntu virtual machine within the same resource group as the Windows 10 VM ensuring that the <b>authentication type</b> is "password" with any credentials. Keep them in mind.
<img src="https://github.com/VTeas2000/azure-network-protocols/assets/60052902/08ba5512-b747-4db0-b83a-3c8d67f522b5" height="80%" width="80%" alt="Ubuntu VM"/>
</p>

<h3>Observe ICMP Traffic and Configure Network Security Groups</h3>
<p>
Use Remote Desktop to connect to your Windows 10 VM through its public IP address.
<br>Within your Windows 10 VM, download and install Wireshark (Windows Intel Installer).
<br>Open Wireshark and select "Ethernet".
<img src="https://github.com/VTeas2000/azure-network-protocols/assets/60052902/4eb8ba85-9bae-4c95-8f84-aab81af7885f" height="80%" width="80%" alt="Wireshark"/>
<br>Filter for ICMP traffic only.<br>
<img src="https://github.com/VTeas2000/azure-network-protocols/assets/60052902/c0734b35-9232-4beb-8bc3-72cca5137e62" height="80%" width="80%" alt="Filter ICMP"/>
<br>Open command prompt and ping your Ubuntu VM's private IP using "ping (ip address)"
<img src="https://github.com/VTeas2000/azure-network-protocols/assets/60052902/53edcbe9-c517-4eee-adeb-c75113679291" height="80%" width="80%" alt="Ping Ubuntu"/>
<br>Observe ping requests and replies within Wireshark.
<img src="https://github.com/VTeas2000/azure-network-protocols/assets/60052902/fa35979c-eb40-43b6-92a9-fe21e894d652" height="80%" width="80%" alt="Observe"/>
<br>Ping a public website such as Google using "ping (website)"
<img src="https://github.com/VTeas2000/azure-network-protocols/assets/60052902/9c1636a1-2dcf-4c2b-a345-c7ed368e9a17" height="80%" width="80%" alt="Ping Website"/>
<br>Observe the traffic in Wireshark.
<img src="https://github.com/VTeas2000/azure-network-protocols/assets/60052902/1c003c22-b6a8-4d63-911d-2f4b7dd1b9a5" height="80%" width="80%" alt="Observe"/>
<br>Perpetually ping your Ubuntu's VM through its private IP using "ping (ip address) -t"
<img src="https://github.com/VTeas2000/azure-network-protocols/assets/60052902/85f5f85a-d1de-4132-861c-0d1385476d83" height="80%" width="80%" alt="Perpetual Ping"/>
<br>Back on Microsoft Azure on your main device, go to your Ubuntu VM's <b>network security group</b> and access its <b>inbound security rules</b>.
<img src="https://github.com/VTeas2000/azure-network-protocols/assets/60052902/d6bc1bb3-74d9-43d8-ab1b-9f09e649e3c2" height="80%" width="80%" alt="Inbound"/>
<br>Add a new inbound security rule with the protocol as "ICMP" and action as "deny".
<img src="https://github.com/VTeas2000/azure-network-protocols/assets/60052902/72e69353-2c72-4a43-b92a-c642fd47c3d0" height="80%" width="80%" alt="Deny ICMP"/>
<br>Back on the Windows VM, notice that the request will time out on the command prompt.
<img src="https://github.com/VTeas2000/azure-network-protocols/assets/60052902/82ef6354-fde8-4ea5-baa1-9f412ce78ee4" height="80%" width="80%" alt="Deny ICMP"/>
<br>No response will be found on Wireshark.
<img src="https://github.com/VTeas2000/azure-network-protocols/assets/60052902/11a07676-6039-47a7-9d05-d6ebd16a396f" height="80%" width="80%" alt="Deny ICMP"/>
<br>On your main device, update the inbound security rule you created to allow ICMP traffic. 
<img src="https://github.com/VTeas2000/azure-network-protocols/assets/60052902/8a0dafb1-8bce-4a30-a14e-ee9308db86a5" height="80%" width="80%" alt="Allow ICMP"/>
<br>Back on the Windows VM, notice that ICMP traffic has been re-enabled. End the perpetual ping in the command prompt using "Ctrl+C"
</p>
