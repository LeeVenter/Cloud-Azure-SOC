# Building a SOC + Honeynet in Azure (Live Traffic)
![Cloud Honeynet / SOC](https://github.com/LeeVenter/Cloud-Azure-SOC/assets/128151666/882558be-8648-46c2-b5bb-d215cade1a77)

## Introduction

In this project, I build a mini honeynet in Azure and ingest log sources from various resources into a Log Analytics workspace, which is then used by Microsoft Sentinel to build attack maps, trigger alerts, and create incidents. I measured some security metrics in the insecure environment for 24 hours, apply some security controls to harden the environment, measure metrics for another 24 hours, then show the results below. The metrics we will show are:

- SecurityEvent (Windows Event Logs)
- Syslog (Linux Event Logs)
- SecurityAlert (Log Analytics Alerts Triggered)
- SecurityIncident (Incidents created by Sentinel)
- AzureNetworkAnalytics_CL (Malicious Flows allowed into our honeynet)

## Architecture Before Hardening / Security Controls
![Architecture Diagram](https://github.com/LeeVenter/Cloud-Azure-SOC/assets/128151666/3b9d48be-0fa5-4e68-832c-5322990d5ad9)

## Architecture After Hardening / Security Controls
![Architecture Diagram](https://github.com/LeeVenter/Cloud-Azure-SOC/assets/128151666/833318e4-d3d0-464b-8549-1917b879acc3)

The architecture of the mini honeynet in Azure consists of the following components:

- Virtual Network (VNet)
- Network Security Group (NSG)
- Virtual Machines (2 windows, 1 linux)
- Log Analytics Workspace
- Azure Key Vault
- Azure Storage Account
- Microsoft Sentinel

For the "BEFORE" metrics, all resources were originally deployed, exposed to the internet. The Virtual Machines had both their Network Security Groups and built-in firewalls wide open, and all other resources are deployed with public endpoints visible to the Internet; aka, no use for Private Endpoints.

For the "AFTER" metrics, Network Security Groups were hardened by blocking ALL traffic with the exception of my admin workstation, and all other resources were protected by their built-in firewalls as well as Private Endpoint

## Attack Maps Before Hardening / Security Controls
![NSG Allowed Inbound Malicious Flows](https://github.com/LeeVenter/Cloud-Azure-SOC/assets/128151666/2cf915e4-71bd-49d6-8649-7783d6c073ff)
<br>
![Linux Syslog Auth Failures](https://github.com/LeeVenter/Cloud-Azure-SOC/assets/128151666/15d8be37-186f-4542-b47e-3f9e548a4fd4)
<br>
![Windows RDP/SMB Auth Failures](https://github.com/LeeVenter/Cloud-Azure-SOC/assets/128151666/7566927c-e992-42f3-84c2-728e8cdb1b05)
<br>
![MsSQL Authentication Fail](https://github.com/LeeVenter/Cloud-Azure-SOC/assets/128151666/0a0b0f33-2396-42a1-a17e-8e2c13992a65)

<br>

## Metrics Before Hardening / Security Controls

The following table shows the metrics we measured in our insecure environment for 24 hours:
Start Time 2023-06-21 16:50:53 
Stop Time 2023-06-22 16:50:53

| Metric                   | Count
| ------------------------ | -----
| SecurityEvent            | 180 452
| Syslog                   | 2278
| SecurityAlert            | 15
| SecurityIncident         | 380
| AzureNetworkAnalytics_CL | 1564

## Attack Maps Before Hardening / Security Controls

```All map queries actually returned no results due to no instances of malicious activity for the 24 hour period after hardening.```

## Metrics After Hardening / Security Controls

The following table shows the metrics we measured in our environment for another 24 hours, but after we have applied security controls:
Start Time 2023-03-18 15:37
Stop Time	2023-03-19 15:37

| Metric                   | Count
| ------------------------ | -----
| SecurityEvent            | 12 082
| Syslog                   | 24
| SecurityAlert            | 0
| SecurityIncident         | 0
| AzureNetworkAnalytics_CL | 0

## Conclusion

In this project, a mini honeynet was constructed in Microsoft Azure and log sources were integrated into a Log Analytics workspace. Microsoft Sentinel was employed to trigger alerts and create incidents based on the ingested logs. Additionally, metrics were measured in the insecure environment before security controls were applied, and then again after implementing security measures. It is noteworthy that the number of security events and incidents were drastically reduced after the security controls were applied, demonstrating their effectiveness.

It is worth noting that if the resources within the network were heavily utilized by regular users, it is likely that more security events and alerts may have been generated within the 24-hour period following the implementation of the security controls.# Cloud-Azure-SOC
