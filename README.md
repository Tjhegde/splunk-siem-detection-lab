# Splunk SIEM Detection & Incident Investigation Lab

**Status: In Progress**

A hands-on cybersecurity lab focused on building a small Splunk SIEM environment, collecting Windows endpoint telemetry, developing detections, and investigating a controlled security incident.

The project is being built incrementally, with configurations, detections, screenshots, and investigation results added as each stage is completed.

## Project Goals

This lab is designed to provide practical experience with common SOC and SIEM workflows, including:

* Deploying and configuring Splunk Enterprise
* Forwarding Windows logs with Splunk Universal Forwarder
* Collecting Windows Security, Sysmon, PowerShell, and Task Scheduler telemetry
* Writing SPL searches and detections
* Creating Splunk alerts and dashboards
* Writing Sigma rules
* Investigating suspicious activity across multiple log sources
* Mapping observed behavior to MITRE ATT&CK
* Documenting findings in an incident report

## Lab Environment

The lab uses two VirtualBox virtual machines connected through an isolated internal network.

| System           | OS               | IP            | Purpose                    |
| ---------------- | ---------------- | ------------- | -------------------------- |
| `SPLUNK-SERVER`  | Ubuntu 24.04 LTS | `10.10.20.10` | Splunk Enterprise SIEM     |
| `WIN11-ENDPOINT` | Windows 11       | `10.10.20.20` | Monitored Windows endpoint |

The Windows endpoint will run:

* Splunk Universal Forwarder
* Sysmon
* Windows Security auditing
* PowerShell logging
* Task Scheduler logging

Telemetry will be forwarded to Splunk for searching, detection, visualization, and investigation.

The systems will be isolated from external networks during incident simulation.

## Controlled Incident Scenario

Once telemetry collection is working, the Windows endpoint will generate a safe simulated incident involving:

* Multiple failed authentication attempts
* A successful authentication
* Creation of a temporary local account
* Addition of that account to the Administrators group
* Harmless encoded PowerShell execution
* Windows system-discovery commands
* Creation of a benign scheduled task

The resulting activity will be analyzed in Splunk and later cleaned up.

No malware is used in this lab.

## Planned Detections

SPL detections will cover activity such as:

* Failed-logon bursts
* Local account creation
* Administrator-group membership changes
* Encoded PowerShell
* Scheduled-task creation
* System-discovery command bursts
* SIEM ingestion and data-quality issues

Selected detections will also be recreated as Sigma rules.

## Investigation

The final investigation will correlate authentication, account-management, process, PowerShell, and scheduled-task telemetry to reconstruct the incident.

The completed project will include:

* Detection results
* A combined incident timeline
* MITRE ATT&CK mappings
* False-positive and detection-limit analysis
* Containment actions
* A written incident report
* Sanitized screenshots and evidence

## Repository Structure

```text
.
├── configs/
│   ├── sysmon/
│   └── splunk-forwarder/
├── scripts/
├── detections/
│   ├── spl/
│   └── sigma/
├── dashboards/
├── docs/
│   ├── ROADMAP.md
│   └── incident-report.md
└── evidence/
    └── screenshots/
```

Some directories may remain empty until the corresponding phase of the project is completed.

## Progress

See [`docs/ROADMAP.md`](docs/ROADMAP.md) for current progress and planned work.

## Security and Privacy

Only sanitized material will be published.

This repository will not contain:

* Passwords or authentication secrets
* Splunk license files
* Session cookies
* VM images or operating-system installation media
* Personal usernames or hostnames
* Unreviewed raw Windows event logs
* Memory dumps
* Sensitive or unrelated host data

## Disclaimer

This is an educational cybersecurity lab performed in an isolated environment using systems that I control.

The simulated activity is intended solely for defensive security, detection-engineering, and incident-investigation practice.
