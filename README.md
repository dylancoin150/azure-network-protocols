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

<h2>High-Level Deployment and Configuration Steps</h2>

- Create Resources in Azure
- Observe ICMP Traffic
- Observe SSH Traffic
- Observe DHCP Traffic
- Observe DNS Traffic
- Observe RDP Traffic
- Cleanup

<h2>Deployment and Observation Steps</h2>

1. Begin by accessing the Azure Portal and navigating to the Resource Groups section. Then, create a new Resource Group named "RG1." This Resource Group will serve as a container for organizing and managing related Azure resources within your Azure subscription.

2. Create a Windows 10 Virtual Machine ("VM1") in the Azure Portal. During the creation process, select the previously created Resource Group ("RG1"); allow the creation of a new Virtual Network (Vnet) and Subnet for VM1.

3. Create an Ubuntu Virtual Machine ("VM2") in the Azure Portal. While setting up VM2, choose the previously created Resource Group ("RG1") for organizational purposes. Connect to the Vnet created with VM1.

4. Access VM1 through Remote Desktop and launch Microsoft Edge on VM1. Navigate to the official website to download Wireshark, a network protocol analyzer.

5. After downloading Wireshark on VM1, proceed to install the application. Follow the installation prompts to complete the installation process successfully.

6. open Wireshark on VM1. Proceed to apply a filter within Wireshark to display only ICMP (Internet Control Message Protocol) traffic. This focused filtering enables the examination of ICMP packets specifically, offering detailed insights into ICMP traffic across the network.

7. In the Azure Portal, locate the Ubuntu VM within the Resource Group "RG1" and find its private IP address in the Networking settings. Return to the VM1 and open the Command Prompt. Type "ping -t [VM2_Private_IP_Address]" and press Enter; replace "[VM2_Private_IP_Address]" with VM2's private IP address. Observe the output, if the Ubuntu VM is reachable and configured correctly, you should receive responses to the ping command, indicating successful network connectivity. Use Ctrl + C to end the ping.

8. Type "ping -t www.google.com" into Command Prompt to initiate a continuous ping to the public website. While the continuous ping is running, switch to Wireshark and observe the traffic. Filter the captured packets to display only ICMP traffic related to the continuous ping to www.google.com. Go back into Command Prompt and use Ctrl + C to end the ping.

9. Start a perpetual ping from VM1 to VM2 by opening Command Prompt and typing "ping -t [VM2_Private_IP_Address]." Then, go to the Azure Portal and find the Network Security Group (NSG) associated with VM2. Disable incoming (inbound) ICMP traffic, return to VM2, and observe the ICMP traffic in Wireshark while filtering for ICMP packets. Additionally, monitor the Command Prompt window to observe the continuous ping activity.

10. Return to the Azure Portal and re-enable ICMP traffic for VM2. Back in VM1, observe the ICMP traffic in Wireshark and the continuous ping activity in the Command Prompt, use Ctrl + C to end the ping.

11. Open Wireshark on VM1, type "ssh" in the filter field, and press Enter. Wireshark will then show only packets related to SSH traffic.

12. Open the Command Prompt on VM1, keeping Wireshark in the background, and initiate an SSH connection to VM2 by typing "ssh [username]@[VM2's IP address]" and pressing Enter. With Wireshark in the background observe the traffic, ensuring that Wireshark is still filtering for SSH packets only. Back in Command Prompt, exit the SSH connection by typing "exit" and pressing Enter.

13. Return to Wireshark and apply a filter to display only DHCP (Dynamic Host Configuration Protocol) traffic by typing "DHCP" in the filter field and pressing Enter. Wireshark will then show only packets related to DHCP traffic.

14. In Command Prompt, type "ipconfig /renew" to request a new IP address from the DHCP server. While the command is executed, observe the DHCP traffic in Wireshark, in the background.

15. Return to Wireshark and apply a filter to display only DNS (Domain Name System) traffic. Open Command Prompt and use "nslookup" to find the IP addresses of "google.com" and "disney.com." While executing the nslookup commands, observe the DNS traffic captured in Wireshark.

16. Back in Wireshark, for the final time, filter for RDP (Remote Desktop Protocol) traffic using the filter "tcp.port == 3389". This filter specifically targets TCP traffic on port 3389, which is the default port used by RDP. Upon applying the filter, you'll observe a continuous stream of traffic in Wireshark. This constant stream of traffic is characteristic of RDP connections, as the protocol facilitates the live streaming of desktop content from one computer to another, resulting in a continuous transmission of data packets.

17. Close the Remote Desktop connection to VM1. In the Azure Portal, delete the Resource Group "RG1" containing all associated resources, including VM1 and VM2. Confirm the deletion of all resources within the Resource Group.

18. After everything is deleted, close the Azure Portal and reopen it to ensure all resources have been successfully deleted. This verification step ensures that the Resource Group, VMs, and any other associated resources have been completely removed from the Azure environment.
