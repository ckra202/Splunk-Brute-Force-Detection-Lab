# Splunk-Brute-Force-Detection-Lab
This project demonstrates how to detect brute-force login attempts against a windows machine using "Splunk Enterprise" and "Hydra". The simulation is conducted in a lab environment with a kali linux attacker and windows 10 target, showcasing real-time log analysis and alerting via Splunk. 

------

# Lab Environment

- Target: Windows 10 VM
- Splunk Enterprise installed locally
- Windows Security Logging Enabled (Event ID 4625)
- Attacker: Kali LInux VM
- Hydra used to simulate brute-force RDP login attempts
- Both VMs networked to allow RDP access
- Splunk used to ingest, search, and visualize failed login logs


-----


# Attack Simulation

Hydra was used from kali linux to brute-force RDP credentials on the windows target.

Command: hydra -t 4 -V -f -l testuser -P passlists.txt rdp://<Windows-IP>


------


# Dashboards

1- Failed Logins Per User 

Shows the number of failed login attempts by username.

SPL Query: index=* source="WinEventLog:Security" EventCode=4625
| stats count by Account_Name
| where count >= 1

![usernames with failed logins attempts](https://github.com/user-attachments/assets/4ae18fac-b702-498c-8760-9eaa0167a75a)
![lab screenshot](https://github.com/user-attachments/assets/97fbeb00-176a-4c8f-9225-5bc62443d749)


------

2- Brute Force Detection Diagram 

SPL Query: 

index=* source="WinEventLog:Security" EventCode=4625
| stats count by Account_Name, Source_Network_Address
| where count >= 5

![brute force running](https://github.com/user-attachments/assets/a8e4ac9d-246b-4496-8cae-6812c253b784)


-------


3- Alert Configuration 

A Splunk alert was created to trigger when a brute-force attempt is detected 

Trigger Condition: 
 * Query returns results
 * Time range: last 5 minutes
 * Alert action: Email

![Login attempt alerts](https://github.com/user-attachments/assets/ce7d1a1a-0c27-44d9-85e2-3c924f6b91a4)


--------

# Lessons Learned

 * The importance of enabling and forwarding Windows security logs
 * Using Hydra safelyin a controlled lab to simulate real-worl attacks
 * Building custom SPL queries to detect attack patterns
 * Creating dashboards and alerts to support SOC workflows

--------

# Credit & Notes

This project was developed as part of a cybersecurity lab portfolio to demonstarte practical detection engineering using free and open-source tools. 




