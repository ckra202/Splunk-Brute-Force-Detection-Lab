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
