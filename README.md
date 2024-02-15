# Building a SOC + Honeynet in Azure (Live Traffic)
![Cloud Honeynet / SOC](https://i.imgur.com/ZWxe03e.jpg)

## Introduction

In this project, I developed a miniature honeynet infrastructure within the Azure environment, integrating diverse log sources into a centralized Log Analytics workspace. This workspace serves as the foundation for Microsoft Sentinel, facilitating the creation of attack maps, alert triggers, and incident management.
The project methodology involved the initial assessment of security metrics within the insecure environment over 24 hours. Subsequently, rigorous security controls were implemented to fortify the environment. Following the hardening phase, another 24-hour metric analysis was conducted to evaluate the efficacy of the applied security measures.

The showcased metrics offer a holistic perspective on the security stance of the environment, both pre-and post-implementation of security controls. These insights serve as a valuable resource for understanding threat detection, optimizing incident response strategies, and enhancing overall resilience.

- SecurityEvent (Windows Event Logs)
- Syslog (Linux Event Logs)
- SecurityAlert (Log Analytics Alerts Triggered)
- SecurityIncident (Incidents created by Sentinel)
- AzureNetworkAnalytics_CL (Malicious Flows allowed into our honeynet)

## Architecture Before Hardening / Security Controls
![Architecture Diagram](https://i.imgur.com/aBDwnKb.jpg)

## Architecture After Hardening / Security Controls
![Architecture Diagram](https://i.imgur.com/YQNa9Pp.jpg)

The architecture of the mini honeynet in Azure consists of the following components:

- Virtual Network (VNet)
- Network Security Group (NSG)
- Virtual Machines (2 Windows, 1 Linux)
- Log Analytics Workspace
- Azure Key Vault
- Azure Storage Account
- Microsoft Sentinel

In the "BEFORE" metrics analysis, all resources were initially deployed and left exposed to the internet. The Virtual Machines had both their Network Security Groups and built-in firewalls configured with open access, while all other resources were deployed with public endpoints accessible from the Internet, rendering private endpoints unnecessary.

In the "AFTER" metrics assessment, Network Security Groups underwent fortification by enforcing a stringent policy, blocking ALL traffic except for connections originating from my designated admin workstation. Furthermore, additional protection was afforded to all other resources through the reinforcement of their built-in firewalls, supplemented by the implementation of Private Endpoints.


## Attack Maps Before Hardening / Security Controls
![NSG Allowed Inbound Malicious Flows](https://i.imgur.com/1qvswSX.png)<br>
![Linux Syslog Auth Failures](https://i.imgur.com/G1YgZt6.png)<br>
![Windows RDP/SMB Auth Failures](https://i.imgur.com/ESr9Dlv.png)<br>

## Metrics Before Hardening / Security Controls

The following table shows the metrics we measured in our insecure environment for 24 hours:
Start Time 2023-03-15 17:04:29
Stop Time 2023-03-16 17:04:29

| Metric                   | Count
| ------------------------ | -----
| SecurityEvent            | 19470
| Syslog                   | 3028
| SecurityAlert            | 10
| SecurityIncident         | 348
| AzureNetworkAnalytics_CL | 843

## Attack Maps Before Hardening / Security Controls

```All map queries returned no results due to no instances of malicious activity for the 24 hours after hardening.```

## Metrics After Hardening / Security Controls

The following table shows the metrics we measured in our environment for another 24 hours, but after we applied security controls:
Start Time 2023-03-18 15:37
Stop Time	2023-03-19 15:37

| Metric                   | Count
| ------------------------ | -----
| SecurityEvent            | 8778
| Syslog                   | 25
| SecurityAlert            | 0
| SecurityIncident         | 0
| AzureNetworkAnalytics_CL | 0

## Conclusion

In this Azure-based project, a mini honeynet was meticulously crafted, with log sources seamlessly integrated into a Log Analytics workspace. Leveraging Microsoft Sentinel, the system adeptly triggered alerts and swiftly addressed incidents based on the processed logs.

A pivotal aspect of the project involved meticulously measuring metrics within the insecure environment before the implementation of security controls. After the fortification measures, a follow-up evaluation of metrics was conducted, showcasing a remarkable reduction in security events and incidents. This significant decrease underscores the efficacy of the implemented security measures.

Furthermore, it's pertinent to acknowledge that in environments where resources are extensively utilized by regular users, there could be a higher frequency of security events and alerts in the 24 hours following the implementation of security controls.
