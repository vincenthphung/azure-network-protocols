<h1 align="center">Inspecting Traffic Between Azure Virtual Machines using NSGs</h1>

<p align="center">
<img src="https://i.imgur.com/Ua7udoS.png" alt="Traffic Examination"/>
</p>

<h2>Introduction</h2>
Network Security Groups (NSGs) in Azure act as a firewall, allowing or denying traffic to resources like Virtual Machines (VMs). This guide provides a detailed walkthrough on monitoring network traffic between Azure VMs using Wireshark and controlling this traffic using NSGs.

<h2>Tools & Technologies</h2>

- **Azure Platform**: Microsoft's cloud computing service for building, testing, deploying, and managing applications and services.
- **Remote Desktop Connection**: A proprietary protocol developed by Microsoft, allowing users to connect to another computer over a network connection.
- **Command-Line Utilities**: Tools available via the command line interface for various tasks.
- **Network Protocols**: Set of rules for data communication. For this guide, we focus on SSH, RDH, DNS, HTTP/S, and ICMP.
- **Wireshark**: A free and open-source packet analyzer used for network troubleshooting and analysis.

<h2>Operating Systems in Use</h2>

- **Windows 10 (Version 21H2)**: A widely used operating system by Microsoft.
- **Ubuntu Server 20.04 LTS**: A free and open-source Linux distribution based on Debian.

<h2>Detailed Steps</h2>

1. **Setting Up the Environment**:
   - **Resource Group**: Acts as a logical container where Azure resources, like VMs, are deployed and managed.
   <img src="https://imgur.com/WgPD275.png" alt="Resource Group Setup"/>
   - **Virtual Machines**: VM1 will be a Windows machine, while VM2 will be an Ubuntu machine. Ensure VM1 has at least 2 vCPUs and 16GB RAM for optimal performance.
   <img src="https://imgur.com/X6ZMTJG.png" alt="VM Setup"/>

2. **Connecting to Windows VM**:
   - Use the Remote Desktop Connection tool to access VM1.
   - Once inside VM1, navigate to the official Wireshark website, download the latest version, and follow the installation prompts.

3. **Filtering ICMP Traffic**:
   - Launch Wireshark on VM1.
   - In the filter bar at the top, type "ICMP" and press enter. This will display only ICMP traffic, making it easier to analyze.
   <img src="https://imgur.com/RrtChUe.png" alt="Wireshark ICMP Filter"/>

4. **Ping Test**:
   - On VM1, open CMD or Powershell.
   - Use the `ping` command followed by the private IP of VM2 to send ICMP packets. This tests the connectivity between the two VMs.
   <img src="https://imgur.com/zmJzyne.png" alt="Ping Test"/>

5. **Continuous Ping & NSG Configuration**:
   - Initiate a continuous ping from VM1 to VM2 using the command `ping <VM2 IP> -t`.
   - In the Azure portal, navigate to the NSG associated with VM2.
   - Block incoming ICMP traffic by adding a new inbound security rule. This will simulate a scenario where VM2 becomes unreachable.
   <img src="https://imgur.com/r3dH3Yy.png" alt="NSG Configuration"/>

6. **Re-enabling ICMP Traffic**:
   - In the Azure portal, modify the NSG rule to allow ICMP traffic again.
   - On VM1, you should observe that the continuous ping resumes successfully.

7. **SSH Traffic Observation**:
   - SSH (Secure Shell) is a protocol used for secure remote login from one computer to another.
   - From VM1, attempt to SSH into VM2. Monitor this SSH traffic in Wireshark for any anomalies or issues.

<h2>Conclusion</h2>
Understanding how to monitor and control network traffic in Azure is crucial for maintaining security and optimal performance. By using tools like Wireshark and Azure's NSGs, administrators can gain valuable insights into their network's operations and ensure a secure environment.



