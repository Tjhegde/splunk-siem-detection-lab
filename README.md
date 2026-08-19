# Splunk SIEM Detection & Incident Investigation Lab

**Project Status: In Progress**

A hands-on cybersecurity lab focused on building a small Security Information and Event Management (SIEM) environment using Splunk, collecting Windows endpoint telemetry, developing detections, and investigating a controlled security incident.

This repository is being developed incrementally. Configuration files, detections, documentation, screenshots, and investigation results will be added as each stage of the lab is completed.

## Project Goals

The goal of this project is to gain practical experience with the tools and workflows commonly used in an entry-level Security Operations Center (SOC).

The completed lab is planned to include:

* Deployment of Splunk Enterprise on an Ubuntu server
* Deployment of a Windows 11 endpoint
* Windows log forwarding with Splunk Universal Forwarder
* Windows Security Event Log collection
* Sysmon telemetry collection
* PowerShell Operational logging
* Task Scheduler logging
* SPL search development
* Detection engineering and alert creation
* Sigma detection rules
* SOC dashboard creation
* Multi-source incident investigation
* MITRE ATT&CK mapping
* False-positive and detection-limitation analysis
* Incident containment
* A documented incident report
* Sanitized screenshots and evidence

## Planned Architecture

The environment will consist primarily of two isolated virtual machines:

```text
                 Internal Lab Network
                    10.10.20.0/24

       ┌──────────────────────────────┐
       │       Splunk Server          │
       │                              │
       │ Ubuntu Linux                 │
       │ Splunk Enterprise            │
       │                              │
       │ Receives and indexes logs    │
       └──────────────▲───────────────┘
                      │
                      │ Splunk Forwarding
                      │
       ┌──────────────┴───────────────┐
       │      Windows Endpoint        │
       │                              │
       │ Windows 11                   │
       │ Splunk Universal Forwarder   │
       │ Sysmon                       │
       │ Windows Event Logs           │
       └──────────────────────────────┘
```

The virtual machines will be isolated from external networks during the controlled incident-generation portion of the lab.

## Planned Telemetry

The Windows endpoint will provide several sources of security telemetry, including:

* Windows Security logs
* Sysmon Operational logs
* PowerShell Operational logs
* Task Scheduler Operational logs
* Windows System and Application logs
* Microsoft Defender logs where applicable

These events will be forwarded to Splunk for searching, correlation, visualization, and investigation.

## Planned Incident Scenario

Once data collection is working, a controlled and non-malicious scenario will be generated on the Windows endpoint.

Planned activity includes:

1. Multiple failed authentication attempts
2. A subsequent successful authentication
3. Creation of a temporary local user
4. Addition of the user to the local Administrators group
5. Execution of a harmless encoded PowerShell command
6. Execution of Windows discovery utilities
7. Creation of a benign scheduled task
8. Investigation of the resulting telemetry
9. Removal of the temporary account and scheduled task

No malware is planned for this lab.

## Planned Detections

SPL detections will be developed for activity such as:

* Failed-logon bursts
* Local account creation
* New accounts added to the Administrators group
* Encoded PowerShell execution
* Scheduled-task creation
* Bursts of system-discovery commands
* SIEM ingestion latency and data-quality issues

Several detections will also be represented as Sigma rules to practice writing SIEM-independent detection logic.

## Planned Investigation

After generating the scenario, the investigation will attempt to reconstruct what occurred by correlating multiple log sources.

The investigation will include:

* Authentication activity
* Account-management events
* Process execution
* PowerShell activity
* Scheduled-task activity
* Parent/child process relationships
* Event timestamps
* User context
* Detection alerts
* Containment actions

The resulting activity will be organized into a combined incident timeline.

## MITRE ATT&CK

Relevant observed behaviors will be mapped to MITRE ATT&CK techniques where appropriate.

The mapping will describe observed behavior rather than treating ATT&CK mappings as proof that an activity was malicious.

## Repository Structure

```text
.
├── architecture/       # Architecture diagrams
├── configs/            # Sysmon and Splunk Forwarder configuration
├── scripts/            # Lab preparation/event-generation scripts
├── detections/
│   ├── spl/            # Splunk SPL detections
│   └── sigma/          # Sigma rules
├── dashboards/         # Dashboard documentation and screenshots
├── docs/               # Roadmap, status, investigation, and reports
└── evidence/
    ├── screenshots/    # Sanitized screenshots
    └── sanitized/      # Reviewed evidence safe for publication
```

## Current Status

The project is currently under active development.

See:

* [`docs/STATUS.md`](docs/STATUS.md) for current progress
* [`docs/ROADMAP.md`](docs/ROADMAP.md) for planned implementation stages

## Security and Privacy

Only sanitized material will be published in this repository.

The repository will not contain any of the following:

* Passwords or credentials
* Splunk authentication secrets
* Session cookies
* Splunk license files
* VM disk images
* Operating-system installation media
* Personal usernames or hostnames
* Unreviewed Windows Event Log exports
* Memory dumps
* Unreviewed raw security telemetry
* Sensitive or unrelated host data

## Disclaimer

This is an educational cybersecurity lab performed in an isolated environment using systems that I control.

The simulated activity is intended solely to generate defensive security telemetry for detection and incident-investigation practice.
