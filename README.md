<h1>Detecting Attacks in Progress Lab</h1>

<h2>Description</h2>
This lab consists of three virtual machines (VM) - a victim, an attacker, and a Wazuh workstation. To detect the attacks I will make, I will first install a SEIM called Wazuh on the victim's VM and update the machine's audit policies to report attempted login events. I will then use the Ncrack tool from the Attacker VM to conduct a brute force attack on the victim VM over telnet. I will be able to detect this attack through the Wazuh-workstation VM. Lastly, I will simulate a DoS attack using hping to the Wazuh-workstation VM and capture this attack through Wireshark.
<br />


<h2>Utilities Used</h2>

- <b>SEIM - Wazuh</b> 
- <b>Wireshark</b>

<h2>Environments Used </h2>

- <b>Windows</b>
- <b>Kali Linux</b>

<h2>Program walk-through:</h2>

<p align="center">
Installing Wazuh <br/>
<br/>
1. Install Wazuh on the Victim machine using the Wazuh agent installer file. This installater file can be found here: https://documentation.wazuh.com/current/installation-guide/wazuh-agent/index.html <br/>
<img src="https://imgur.com/s18SzeI.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
2. Find the Wazuh agent file through the File Explorer: Computer --> Local Disk (C:) --> Program Files --> ossec-agent <br/>
<img src="https://imgur.com/GmAKTWG.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
3. Open the folder and right click on win32ui to Run as administrator. Enter the Wazuh server IP address, 192.168.57.20, when the manager opens. Make sure to press Save. <br/>
<img src="https://imgur.com/2KjPNGM.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
4. Restart the Wazuh service. Using cmd and running it as administrator, enter the following command: net start wazuhsvc.  <br/>
<img src="https://imgur.com/L1QbduL.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
5. After the service starts, go back to the Wazuh Agent Manager and press Refresh. An Authentication key will generate below the Manager IP. This confirms that the agent on the Victim’s machine is registered with the Wazuh server. <br/>
<img src="https://imgur.com/NXWV0Tf.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br /> 
Updating Audit Policies and Enabling Telent <br/>
<br/>
6. To monitor the login events of the Victim, update the machine’s local group policy and enable the audit logon events. Start this by searching for gpedit.msc in the start menu and clicking gpedit when it appears. <br/>
<br />
7. Find Audit account logon events through Computer Configuration --> Windows Settings --> Security Settings --> Local Policies --> Audit Policy. Double click it and check both Success and Failure audit attempt events. Press Apply and OK. Repeat this for Audit logon events. <br/>
<img src="https://imgur.com/xbTZQau.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />   
8. Force update the policy changes through the command prompt using the command gpupdate /force.  <br/>
<img src="https://imgur.com/CUgp485.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
9. Time to enable Telnet. Click on the FreeSSHd tool on the desktop. Ignore the error message and open the SSH tool from the taskbar. Start the Telnet server.   <br/>
<img src="https://imgur.com/dkUDthP.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br /> 
Wazuh Dashboard <br/>
<br/>
10.	On the Wazuh-workstation machine, open Google Chrome and enter the Wazuh dashboard IP address: https://192.168.57.20. Chrome will warn that the connection is not private (due to it not being a published website). Select Advanced and Proceed to 192.168.57.20 (unsafe). Once the page is loaded, enter the username admin and password P*ssw0rd. <br/>
<img src="https://imgur.com/lEh9dur.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br /> 
11.	Click on Active agents to confirm that the Victim’s agent has been added. Click on the agent to be directed to the agent’s specific events page. <br/>
<img src="https://imgur.com/kn2P41S.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br /> 
Detecting Attacks in Progress <br/>
<br/>
</p>

<!--
 ```diff
- text in red
+ text in green
! text in orange
# text in gray
@@ text in purple (and bold)@@
```
--!>
