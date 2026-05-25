# Deployment and Integration of Wazuh SIEM

## Objective
[Brief Objective]

This projects onjective is to deploy and configure a security monitoring environment using Wazh SIEM to collect, analyse and visualise security events from endpoint systems. The aim of this lab is to demonstrate how security logs can be monitored and correlated to identify suspicious activity such as failed logins, priviledge escalation and potential brute force attacks. This project also focuses on building a basic SOC style dashboard to improve visibility into security events and support incident detection and analysis.

## Skills Learned

- Deployed and configured Wazuh SIEM for security monitoring
- Log collection and event processing from endpoint systems
- Created detection rules and interpreted generated alerts
- correlation of security events to identify potential attack patterns
- Building and customising SOC style dashboards for visualising security data
- Basic incident investigation using alert details such as IP address, timestamp, and rule ID
- Developed foundational SOC analyst skills, including threat identification and reporting
- 
## Tools Used

- Wazuh - primary SIEM platform for collecting, analysing and visualising security logs from endpoint systems
- Windows Operating System - Endpoint to generate authentication events and security logs
- Kali Linux - generated and tested security events such as SSH and priviledge escalation activity
- VirtualBox - Host multiple virtual machines for lab environment
- Web Browser - used to access Wazuh dashboard and investigate alerts and events

## Steps

### SIEM Platfrom

I successfully accessed the Wazuh SIEM dashboard to ensure that the centralised monitoring platform was functioning correctly. The SIEM dashboard includes centralised event monitoring, endpoint visibility, threat detection workflows, SOC monitoring capabilities and, security alert visualisation. This shows that SIEM infrastructure is operational and provides real time security monitoring.  

Wazhu Dashboard:

<img width="1916" height="876" alt="image" src="https://github.com/user-attachments/assets/c2bc96d3-4904-424a-bb2c-c499a8aec885" />

### Verifying Endpoint Connectivity

After successfully deploying the endpoint agent, we verified the connectivity to the centralized Wazuh SIEM server through the agent management interface. The Windows 11 endpoint was confirmed to be active in the dashboard. This showed that it was successfully maintaining stable communication with the Wazuh Manager. 

Agents Connected:

<img width="1907" height="747" alt="image" src="https://github.com/user-attachments/assets/774d7cb7-1a3a-40bf-aca3-9f2f88415b47" />

### Log Ingestion and Real Time Event Verification

To test whether the logs were successfully ingested into the Wazuh SIEM platform, we reviewed the security events dashboard. The Windows endpoint showed security related events being sent to SIEM which indicates that the logs forwading between the agent and the manager were working correctly.

Live Events Stream:

<img width="1911" height="872" alt="image" src="https://github.com/user-attachments/assets/d1ab3477-0489-4f8d-8361-813bcf2b0b7e" />

Events were seen updating in real time  in the security events section indicating that the system was actively recieving and processing data from the connected endpoint. The data included basic system and security events generated through normal activity on the machine. To confirm the accuracy of log collection, we will generate additional user activity on the endpoint to verify that events are captured and displayed correctly within the Wazuh SIEM platfrom. 

### Baseline Testing (Normal User Activity)

To simulate normal user behaviour, we performed standard activity such as opening a web browser, accessing system settings, and performing normal user login sessions on the Windows endpoint. These measures generated expected endpoint activity during everyday system use. 

Once these measures were performed, we reviewed the Wazuh SIEM Security Events dashboard to confirm whether the corresponding logs were being generated and collected in real time. 

Normal Activity Logs:
<img width="1898" height="867" alt="image" src="https://github.com/user-attachments/assets/1a254b3b-b068-4b4f-bf2e-c3af6d88af86" />

The endpoint was observed sending regular system and security events which confirms that user driven activity is being successfully captured by SIEM. Activity such as web browsing and system interactions generated proccess creation event within SIEM. This behaviour is expected as user actions generate multiple proccesses in modern operating systems. This confirms that the log collection process is funtioning correctly for normal user behaviour and the system recorded and displayed the endpoint activity. We wilol use this baseline as a reference point for identifying suspicious and abnormal behaviour in the lab environment.

### Attack Simulation

A series of authentication events were performed on the endpoint to simulate potentical brute force and priveledge escalation activity. This included failed login attempts using incorrect passowrds and usernames which was followed by successful authentication sessions and a priveledge escalation using sudo.

Alerts triggered:

<img width="1911" height="873" alt="image" src="https://github.com/user-attachments/assets/2f752b6f-ddb7-43ed-9a83-16e57f9b9775" />

<img width="1913" height="342" alt="image" src="https://github.com/user-attachments/assets/37448afd-5730-4b30-930c-2d49bf95c82c" />

Wazuh SIEM captured authentication failures and successful priveledge elevation events which demonstrates visibility across multiple stages of an attack cycle. This includes credential guessing, successful access and escalation to root priveledges. 

### Multi-Event Security Investigation

To investigate the security events we selected the alerts from Wazuh SIEM dashboard and expanded them to analyze them in detail. The alerts provide forensic key information such as the source of the event, the target machine, the timestamp, the rule ID, and the assigned severity level.

Alert Details Expanded (Logon Failure):

<img width="591" height="815" alt="image" src="https://github.com/user-attachments/assets/94e3e88d-09ee-4ea2-bfa6-ccc02afc723f" />
<img width="611" height="801" alt="image" src="https://github.com/user-attachments/assets/bd952943-2aab-4257-b734-90259e994b9f" />

The alert confirms a Windows authentication failure within the Wazuh SIEM using Discover. This corresponded to a failed login attempt (Event ID 4625), which was generated on Windows endpoint. The log contained forensic information such as source system, target host, logon type, failure reason, and status code. The status code (0xC000006D) verifies that the authentication attempt was unsuccessful due to incorrect credentials. 

Alert Details Expanded (Successful Login):

<img width="870" height="787" alt="image" src="https://github.com/user-attachments/assets/46913b3b-2f7a-4575-ba35-650fd4c06cb1" />
<img width="598" height="157" alt="image" src="https://github.com/user-attachments/assets/aea708e5-73f9-4661-9b65-8f3aba2d4106" />

The alert confirms that the user 'jacked' has successfully authenticated and opened a root session by the PAM authentication system. This was then followed by administrative activity which affected system configuration files. This event was classified as authentication success and priviledge escalation activity which mapped to MITRE ATT&CK technique T1078 (Valid accounts). This shows that Wazuh provides visibility into priviledge session creation and administrative actions performed.

Alert Details Expanded (Priviledge Escalation):

<img width="1066" height="763" alt="image" src="https://github.com/user-attachments/assets/ffee39e9-8dcc-403a-9637-9d037ef5eec8" />
<img width="411" height="192" alt="image" src="https://github.com/user-attachments/assets/a26d203c-6194-42a4-bb0a-0fd1fcf5fe40" />

The alert shows that the user 'jacked' has successfully escalated priviledges using sudo and accessed the Wazuh rules configuration file. This activity was mapped to MITRE ATT&CK techniques T1548.003 (Sudo and Sudo Cashing) which indicates priviledge escalation behaviour. 

This investigation overall demonstrates Wazuh platforms ability to centralise security events and provide detailed information which is required for SOC analysis and incident triage.

### Event Correlation and Pattern Detection

We then analysed the security events in the Wazuh interphase to identify potential attack points. To analyse this, we filtered the authentication failure logs by rule ID and source IP address over the past 24 hours.

Correlation Views:

<img width="1912" height="813" alt="image" src="https://github.com/user-attachments/assets/3eea186c-c4a4-4c1c-b50b-8f23fe2b81bd" />

The results show repeated failed login attempts coming from the same source within a short timeframe. This patterns indicates potential brute force or credential guessing behaviour. Multiple events across time where correlated with source attributes to distinguish between isolated login failures and repeated suspicious authentication activity. This shows that SIEM tools support behavioural based threat detection rather than individual event analysis.

### SOC Dashboard 

We created a SOC dashboard in Wazuh to visualise and monitor security events. The dashboard presents key security metrics in a clear and attainable way. To show failed login attempts over time we created a line chart and to source the top IP addresses involved in suspicious activity, we demonstrated it in a bar chart.We also created a pie chart to represent the distribution of different types of security alerts based on severity and event category. The dashboard allowed us to convert raw log data into meaningful visual insights. This makes it easier to identify patterns and potential security threats within the environment. 

SOC Dashboard:

<img width="1917" height="871" alt="image" src="https://github.com/user-attachments/assets/945d188d-55fd-4886-abcf-a6b906ae7ebd" />



### References

1. MITRE (2025). MITRE ATT&CK. [online] Mitre.org. Available at: https://attack.mitre.org/.
2. Wazuh (2024). Wazuh documentation. [online] documentation.wazuh.com. Available at: https://documentation.wazuh.com/current/index.html.
