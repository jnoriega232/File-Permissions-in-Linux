# File Permissions in Linux

## Project Description
The research team in the fictional organization I'm describing is in the process of revising the file permissions for specific files and directories located within the  ```projects``` directory. The existing permissions do not accurately align with the intended level of authorization. Ensuring that these permissions are reviewed and adjusted appropriately is crucial for maintaining the security of their system. To achieve this objective, I undertook the following actions:

## Check File and Directory Details
The provided code exemplifies my utilization of Linux commands to ascertain the current permissions configured for a particular directory within the file system.

<p align="center">
<img src="https://i.imgur.com/LgGnWj5.png" height="80%" width="80%" alt="Azure Free Account"/>

In the screenshot, the initial line showcases the command I input, while subsequent lines exhibit the resulting output. The code comprehensively enumerates the items within the ```projects``` directory. I employed the ```ls``` command with the ```-la``` option to reveal an elaborate list of file contents, encompassing hidden files. The output of my execution discloses the presence of a directory named ```drafts```, a concealed file labeled ```.project_x.txt```, and five additional project files. The initial 10-character string in the first column symbolizes the permissions designated for each individual file or directory.

## Describe the Permissions String
The 10-character sequence can be dissected to discern the individuals with authorized access to the file and their respective permissions. The characters have the following interpretations:

- 1st Character: A ```d``` or hyphen (```-```) signifies the file type. ```d``` indicates a directory, while (```-```) indicates a regular file.

- 2nd-4th Characters: These characters denote the user's read (```r```), write (```w```), and execute (```x```) permissions. A hyphen (```-```) signifies the absence of the corresponding permission.

- 5th-7th Characters: These characters denote the group's read (```r```), write (```w```), and execute (```x```) permissions. A hyphen (```-```) signifies the absence of the respective permission.

- 8th-10th Characters: These characters denote the "other" category's read (```r```), write (```w```), and execute (```x```) permissions. This category encompasses all users aside from the user and the group. A hyphen (```-```) indicates the lack of the specified permission.

As an illustration, let's take the file permissions of ```project_t.txt``` as an instance: ```-rw-rw-r--```. With a hyphen (```-```) as the first character, it's evident that ```project_t.txt``` is a file rather than a directory. The presence of ```r``` in the second, fifth, and eighth positions signifies that the user, group, and others possess read permissions. The third and sixth positions bear ```w```, indicating that exclusively the user and group hold write permissions. Notably, no entity has execute permissions for ```project_t.txt```.

## Change File Permissions
The organization concluded that no write access should be granted to "other" for any of their files. To align with this directive, I revisited the file permissions I had previously retrieved. Upon analysis, I identified that write access for "other" needs to be revoked from ```project_k.txt```.

The subsequent code exemplifies my utilization of Linux commands to accomplish this task:

<p align="center">
<img src="https://i.imgur.com/hq5GtTH.png" height="80%" width="80%" alt="Azure Free Account"/>

The initial pair of lines within the screenshot showcases the commands I input, while the subsequent lines present the outcome of the second command. Utilizing the ```chmod``` command, permissions on files and directories are modified. The first argument dictates the permissions to be altered, and the second argument designates the file or directory. In this instance, I eliminated write permissions for "other" on the ```project_k.txt``` file. Following this adjustment, I employed ```ls -la``` to assess the modifications I implemented.

## Change File Permissions on a Hidden File
![Architecture Diagram](https://i.imgur.com/uzwHvLp.png)

<b>Prior to implementing hardening measures and security controls:</b>

- During the initial phase of the project ("BEFORE" stage), all resources were deployed with deliberate exposure to the public internet. This deliberate lack of security was intended to entice potential cyber attackers and study their methodologies. The Virtual Machines had both their Network Security Groups (NSGs) and built-in firewalls configured to allow unrestricted access from any source. Furthermore, all other resources, including storage accounts and databases, were deployed with publicly accessible endpoints, without the utilization of Private Endpoints for enhanced security.

## Architecture After Hardening / Security Controls
![Architecture Diagram](https://i.imgur.com/EEuwLHJ.png)

<b>In the "AFTER" stage, I implemented a series of measures to fortify the environment's security and enhance its overall posture. The key improvements implemented include:</b>

- <b>Strengthening Network Security Groups (NSGs)</b>: I reinforced the NSGs by implementing a restrictive policy that blocked all inbound and outbound traffic, with the exception of my own public IP address. This ensured that only authorized traffic from a trusted source was granted access to the virtual machines.

- <b>Configuring Built-in Firewalls</b>: I fine-tuned the configurations of the built-in firewalls on the virtual machines to impose restrictions on access, safeguarding the resources against unauthorized connections. By customizing the firewall rules based on the specific requirements of each virtual machine, I minimized the potential attack surface.

- <b>Implementing Private Endpoints</b>: I bolstered the security of other Azure resources by replacing their public endpoints with Private Endpoints. This strategic shift restricted access to sensitive resources, such as storage accounts and databases, to within the virtual network, eliminating exposure to the public internet. This approach provided an additional layer of protection, guarding against unauthorized access and potential attacks.

By conducting a comparative analysis of the security metrics before and after implementing these hardening measures and security controls, I effectively demonstrated the tangible enhancements made to the overall security posture of the Azure environment.

## Attack Maps Before Hardening / Security Controls


- <b>The depicted attack map vividly illustrates the ramifications of maintaining an open Network Security Group (NSG), enabling unhindered passage of malicious traffic. This visual representation serves as a powerful reminder of the criticality of deploying robust security measures, including stringent NSG rule restrictions, to thwart unauthorized access and mitigate potential threats effectively.</b>
![NSG Allowed Inbound Malicious Flows](https://i.imgur.com/A1sRZgz.png)<br>

 - <b>The showcased attack map brings attention to the multitude of syslog authentication failures encountered by the deployed Linux server, signifying unauthorized access attempts originating externally. This serves as a powerful reminder of the utmost significance in fortifying Linux servers with robust authentication mechanisms and diligently monitoring system logs for indications of intrusion endeavors.</b>
![Linux Syslog Auth Failures](https://i.imgur.com/2XLw6g5.png)<br>

- <b>The presented attack map highlights a significant number of RDP and SMB failures, revealing the persistent efforts of potential attackers to exploit these protocols. This visualization effectively underscores the imperative nature of securing remote access and file sharing services, aiming to safeguard against unauthorized access and mitigate potential cyber threats.</b>
![Windows RDP/SMB Auth Failures](https://i.imgur.com/vqAwad9.png)<br>

## Attack Maps After Hardening / Security Controls

```All map queries actually returned no results due to no instances of malicious activity for the 24 hour period after hardening.```

## Metrics Before Hardening / Security Controls

The following table shows the metrics we measured in our insecure environment for 24 hours:
Start Time 2023-05-04 21:55:50
Stop Time 2023-05-05 21:55:50

| Metric                   | Count
| ------------------------ | -----
| SecurityEvent (Windows VM)           | 23146
| Syslog (Linux VM)                  | 2123
| SecurityAlert (Microsoft Defender for Cloud)           | 10
| SecurityIncident (Sentinel Incidents)        | 267
| NSG Inbound Malicious Flows Allowed | 865

## Metrics After Hardening / Security Controls

The following table shows the metrics we measured in our environment for another 24 hours, but after we have applied security controls:
Start Time 2023-05-10 17:38:04
Stop Time	2023-05-11 17:38:04

| Metric                   | Count
| ------------------------ | -----
| SecurityEvent (Windows VM)           | 17718
| Syslog (Linux VM)                  | 24
| SecurityAlert (Microsoft Defender for Cloud)           | 0
| SecurityIncident (Sentinel Incidents)        | 0
| NSG Inbound Malicious Flows Allowed | 0

## Conclusion

Throughout this project, I successfully orchestrated the creation of a honeynet using Microsoft Azure. Subsequently, I diligently performed comprehensive logging and monitoring to detect and respond to any attacks targeting the virtual machines. Moreover, I meticulously analyzed these incidents to gain deeper insights into the tactics, techniques, and procedures employed by the attackers. Finally, I fortified the environment by implementing stringent security controls in alignment with regulatory compliance standards such as NIST 800-53 and NIST 800-61.

The comparative analysis of pre- and post-implementation metrics revealed a notable reduction in security events and incidents, underscoring the effectiveness of the implemented security controls. It is important to note that in scenarios where the network's resources were extensively utilized by regular users, a higher number of security events and alerts may have been generated within the 24-hour timeframe following the implementation of security controls.

This project has been an invaluable learning experience, reinforcing the paramount importance of maintaining robust security. It serves as a stark reminder of the significance of implementing appropriate security controls and configurations to safeguard valuable resources. The stark contrast between an insecure and a secure environment, as highlighted by the before and after metrics, underscores the criticality of implementing measures such as firewall rules, private endpoints, and restricted public internet access to mitigate the potentially catastrophic consequences of attacks and unauthorized access.
