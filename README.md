<p align="center">
<img src="https://i.imgur.com/pU5A58S.png" alt="Microsoft Active Directory Logo"/>
</p>

<h1>On-premises Active Directory Deployed in the Cloud (Azure)</h1>
This guide outlines the implementation of on-premises Active Directory within Azure Virtual Machines.<br />

<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- Active Directory Domain Services
- PowerShell

<h2>Operating Systems Used </h2>

- Windows 10 (21H2)

Azure Network Security Groups - https://docs.microsoft.com/en-us/azure/virtual-network/network-security-groups-overview

Step 1: Create Resources
- Create a Resource Group
- Create a Windows 10 Virtual Machine (VM)
    While creating the VM, select the previously created Resource Group
    While creating the VM, allow it to create a new Virtual Network (Vnet) and Subnet
- Create a Linux (Ubuntu) VM
    While create the VM, select the previously created Resource Group and Vnet
- Observe Your Virtual Network within Network Watcher

Step 2: Observe Traffic
- ICMP Traffic
    Use Remote Desktop to connect to your Windows 10 Virtual Machine
    Within your Windows 10 Virtual Machine, Install Wireshark
    Open Wireshark and filter for ICMP traffic only
    Retrieve the private IP address of the Ubuntu VM and attempt to ping it from within the Windows 10 VM
      Observe ping requests and replies within WireShark
    From The Windows 10 VM, open command line or PowerShell and attempt to ping a public website (such as www.google.com) and observe the traffic in WireShark
    Initiate a perpetual/non-stop ping from your Windows 10 VM to your Ubuntu VM
      Open the Network Security Group your Ubuntu VM is using and disable incoming (inbound) ICMP traffic
      Back in the Windows 10 VM, observe the ICMP traffic in WireShark and the command line Ping activity
      Re-enable ICMP traffic for the Network Security Group your Ubuntu VM is using
      Back in the Windows 10 VM, observe the ICMP traffic in WireShark and the command line Ping activity (should start working)
      Stop the ping activity
 - SSH Traffic
    Back in Wireshark, filter for SSH traffic only
    From your Windows 10 VM, “SSH into” your Ubuntu Virtual Machine (via its private IP address)
      Type commands (username, pwd, etc) into the linux SSH connection and observe SSH traffic spam in WireShark
      Exit the SSH connection by typing ‘exit’ and pressing [Enter]
 - DHCP Traffic
    Back in Wireshark, filter for DHCP traffic only
    From your Windows 10 VM, attempt to issue your VM a new IP address from the command line (ipconfig /renew)
      Observe the DHCP traffic appearing in WireShark
 - DNS Traffic
    Back in Wireshark, filter for DNS traffic only
    From your Windows 10 VM within a command line, use nslookup to see what google.com and disney.com’s IP addresses are
      Observe the DNS traffic being show in WireShark
 - RDP Traffic
    Back in Wireshark, filter for RDP traffic only (tcp.port == 3389)
    Oserve the immediate non-stop spam of traffic? Why do you think it’s non-stop spamming vs only showing traffic when you do an activity?
      Answer: because the RDP (protocol) is constantly showing you a live stream from one computer to another, therefor traffic is always being transmitted

<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>

<br />
