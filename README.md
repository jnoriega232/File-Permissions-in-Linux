# File Permissions in Linux

## Project Description
The research team in the fictional organization I'm describing is in the process of revising the file permissions for specific files and directories located within the  ```projects``` directory. The existing permissions do not accurately align with the intended level of authorization. Ensuring that these permissions are reviewed and adjusted appropriately is crucial for maintaining the security of their system. To achieve this objective, I undertook the following actions:

## Check File and Directory Details
The provided code exemplifies my utilization of Linux commands to ascertain the current permissions configured for a particular directory within the file system.

<p align="center">
<img src="hhttps://i.imgur.com/LgGnWj5.png" height="70%" width="70%" alt="Azure Free Account"/> 
</p>

## Technologies, Regulations, and Azure Components Employed:
- Utilization of Azure Virtual Network (VNet)
- Implementation of Azure Network Security Group (NSG)
- Deployment of Azure Virtual Machines (2x Windows, 1x Linux)
- Creation of a Log Analytics Workspace with Kusto Query Language (KQL) Queries
- Adoption of Azure Key Vault for Secure Secrets Management
- Establishment of an Azure Storage Account for Data Storage
- Integration of Microsoft Sentinel for Security Information and Event Management (SIEM)
- Utilization of Microsoft Defender for Cloud to Protect Cloud Resources
- Incorporation of Windows Remote Desktop for Remote Access
- Utilization of Command Line Interface (CLI) for System Management
- Utilization of PowerShell for Automation and Configuration Management
- Adherence to NIST SP 800-53 Revision 4 for Security Controls
- Implementation of NIST SP 800-61 Revision 2 for Incident Handling Guidance

## Process
- <b>*Establishing the honeynet*</b>: To simulate an insecure environment, I commenced by deploying multiple vulnerable virtual machines within Azure.

- <b>*Monitoring and analysis*</b>: I configured Azure to gather log data from various resources and consolidate them in a log analytics workspace. Leveraging Microsoft Sentinel, I constructed attack maps, triggered alerts, and generated incidents based on the acquired data.

- <b>*Measuring security metrics*</b>: Throughout a 24-hour period, I diligently monitored the environment, documenting critical security metrics while it remained in an insecure state. This provided a benchmark for comparison against the metrics observed after implementing remedial measures.

- <b>*Incident response and remediation*</b>: Upon addressing the identified incidents and vulnerabilities, I embarked on the process of fortifying the environment. This involved implementing security best practices and following Azure-specific recommendations.

- <b>*Post-remediation analysis*</b>: To evaluate the effectiveness of the implemented measures, I conducted another 24-hour observation of the environment. By comparing the resulting security metrics with the initial baseline, I gauged the impact of the remediation efforts.

## Architecture Before Hardening / Security Controls
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
