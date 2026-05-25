# Deployment-and-Integration-of-Wazuh-SIEM-

## Objective
[Brief Objective]

## Skills Learned

## Tools Used

## Steps

### SIEM Platfrom

I successfully accessed the Wazuh SIEM dashboard to ensure that the centralised monitoring platform was functioning correctly. The SIEM dashboard includes centralised event monitoring, endpoint visibility, threat detection workflows, SOC monitoring capabilities and, security alert visualisation. This shows that SIEM infrastructure is operational and provides real time security monitoring.  

Wazhu Dashboard:

<img width="1916" height="876" alt="image" src="https://github.com/user-attachments/assets/c2bc96d3-4904-424a-bb2c-c499a8aec885" />

# Verifying Endpoint Connectivity

After successfully deploying the endpoint agent, we verified the connectivity to the centralized Wazuh SIEM server through the agent management interface. The Windows 11 endpoint was confirmed to be active in the dashboard. This showed that it was successfully maintaining stable communication with the Wazuh Manager. 

Agents Connected:

<img width="1907" height="747" alt="image" src="https://github.com/user-attachments/assets/774d7cb7-1a3a-40bf-aca3-9f2f88415b47" />

# Log Ingestion and Real Time Event Verification

To test whether the logs were successfully ingested into the Wazuh SIEM platform, we reviewed the security events dashboard. The Windows endpoint showed security related events being sent to SIEM which indicates that the logs forwading between the agent and the manager were working correctly.

Live Events Stream:

<img width="1911" height="872" alt="image" src="https://github.com/user-attachments/assets/d1ab3477-0489-4f8d-8361-813bcf2b0b7e" />

Events were seen updating in real time  in the security events section indicating that the system was actively recieving and processing data from the connected endpoint. The data included basic system and security events generated through normal activity on the machine. To confirm the accuracy of log collection, we will generate additional user activity on the endpoint to verify that events are captured and displayed correctly within the Wazuh SIEM platfrom. 

# Baseline Testing (Normal User Activity)

To simulate normal user behaviour, we performed standard activity such as opening a web browser, accessing system settings, and performing normal user login sessions on the Windows endpoint. These measures generated expected endpoint activity during everyday system use. 

Once these measures were performed, we reviewed the Wazuh SIEM Security Events dashboard to confirm whether the corresponding logs were being generated and collected in real time. 

