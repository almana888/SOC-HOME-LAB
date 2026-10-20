# SOC-HOME-LAB
*A home lab simulating SMB brute-force and password spraying attacks, detected and analyzed using Splunk SIEM.*

## Overview
This project is a hands-on home lab built to simulate, detect, and analyze SMB-based credential attacks — specifically Brute Force and Password Spraying — using Splunk Enterprise as the SIEM platform.

The goal was to build a small, self-contained environment that mirrors how attacks and detection work in a real SOC: an attacker machine, a vulnerable target, and a centralized logging system, all communicating over a local network.

Beyond the technical setup, this project was a practical step in my self-study path toward a SOC Analyst role — giving me hands-on experience deploying a SIEM, analyzing real authentication logs, and troubleshooting issues like an actual analyst would.

## Lab Architecture
Three VMs on an isolated local network, simulating SMB brute-force and password spraying attacks against a Windows host, detected via Splunk.
- Attacker: Kali Linux 2026.2 — NetExec (nxc) for brute-force & password spraying
- Victim: Windows 10 — Sysmon 15.21 + Splunk Universal Forwarder
- SIEM: Ubuntu 24.04.5 LTS — Splunk Enterprise 10.6.0.5

![Network Topology](topology.svg)

## Lab Setup

- Installed Splunk Enterprise on Ubuntu, enabled receiving on port 9997.
![Splunk Enterprise Installed](images/splunk-installed.png)

- Installed Splunk Universal Forwarder on Windows 10, pointed to 192.168.1.102:9997.
![Universal Forwarder Setup](images/forwarder-setup.png)

- Configured inputs.conf on the Forwarder to collect Security, System, and Sysmon logs into index=windows_logs.
![inputs.conf Configuration](images/inputs-conf.png)

- Verified log flow in Splunk: index="windows_logs" EventCode=4625.
![Log Verification in Splunk](images/log-verification.png)
