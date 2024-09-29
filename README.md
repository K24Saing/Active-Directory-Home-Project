# Active Directory Home Project
## Objective

The Active Directory Detection Home Lab project aimed to establish a real-world environment for simulating and detecting cyber attacks. The primary focus was to ingest and analyze logs within a Security Information and Event Management (SIEM) system, generating test telemetry to mimic real attack scenarios. This hands-on experience was designed to deepen my technical understanding of network security, attack patterns, and defensive strategies.

### Skills Learned

- Advanced understanding of SIEM concepts and practical application.
- Learned how to create virtual servers, hosts, and SIEM environments.
- Set static IP addresses for each server and host to establish a flow of traffic to the SIEM.
- Ability to generate and recognize real-world attacks using tests from Atomic Red Team.
- Enhanced knowledge of security event telemetry and analysis.
- Development of critical thinking and problem-solving skills in cybersecurity.
- Created an Active Directory Domain with groups and users & forwarded security event traffic to SIEM.

### Tools Used

- Security Information and Event Management (SIEM) system for log ingestion and analysis // Splunk.
- Simulation of Attacks from the MITRE ATT&CK Framework // AtomicRedTeam.
- Setting up virtual environment for home project // VirtualBox.
- Gained knowledge of using operating systems // Kali Linux, Windows Server 2022, Windows 10 Home.

## Steps

![Active Directory Diagram drawio](https://github.com/user-attachments/assets/f0e9f238-7c3f-4416-b4b2-2c0b6b38a1b7)
1. I created a virtual network using VirtualBox with VMs using Windows 10 Server, Pro, Kali Linux, and an Ubuntu Splunk Server with the correct static IP addresses.
2. Configured each machine's network setting to be grouped under the same NAT network using IP address 192.168.10.0/24.
3. Installed Splunk on Ubuntu server using the Splunk website. 
4. Installed Splunk Forwarder and Sysmon on Windows 10 Server and Pro.
5. Configured the inputs.conf file on both Windows Machines to forward "WindowsEventsLog: Security, Application, Sysmon, and System" to index: endpoint.
<table style="width: 100%;">
  <tr>
    <td style="text-align: center;">
      <img src="https://i.postimg.cc/gjfpJmnw/Screenshot-2024-09-29-055534.jpg" alt="Description" style="width: 200px;">
    </td>
  </tr>
</table>
6. Restarted SplunkForwarder & Sysmon64 service with local account. <br>
7. I configured the receiving port to start receiving data from both Windows Machines on Splunk.<br>
8. On the Windows Server, I installed Active Directory Domain Services (ADDS) and promoted it as a domain controller.<br>
9. Added a new user to the Active Directory and configured the Windows 10 Pro machine to join to the domain controller's DNS server. Logged in as the new user from the Active Directory.<br>
10. On my Kali Linux machine, I made a new directory called "ad-project" and copied the "rockyou.txt" file that comes with Kali Linux into the new directory. I then imported the first 20 linws of rockyou.txt and saved it as a new file called passwords.txt.<br>
11. Using nano text editor for Linux, I added the password of my new user account on my Windows 10 Pro machine to the passwords.txt <br>
12. I enabled RDP connections to the target Windows 10 Pro Machine, and ran hydra -b rdp -u {user account name} passwords.txt -s {target IP address} <br>
13. After RDP success, I confirmed the log event in my splunk with EventCode: 4624 for successful log ins. <br>
14. On my Windows 10 Pro target machine, I installed Atomic Red Team following the documentation provided on the Atomic Red Team website. <br>
15. Using the command Invoke-AtomicTest with the appropriate MITRE ATT&CK technique file, I was able to generate a MITRE Attack test on my target machine. <br> 
16. Since WindowsEventsLogs were forwarded to Splunk from my target machine, the Atomic Red Team test was able to generate that event in Splunk for me to observe including the new user that was used in Active Directory.<br>
<table style="width: 100%;">
  <tr>
    <td style="text-align: center;">
      <img src="https://i.postimg.cc/8k7WcG5t/Screenshot-2024-09-29-072103.jpg" alt="Description 1" style="width: 200px;">
    </td>
    <td style="text-align: center;">
      <img src="https://i.postimg.cc/v8Cn6KxM/Screenshot-2024-09-29-071956.jpg" alt="Description 2" style="width: 200px;">
    </td>
  </tr>
</table>




