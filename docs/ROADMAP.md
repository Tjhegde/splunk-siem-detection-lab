# Project Roadmap

This roadmap tracks the development of the Splunk SIEM Detection & Incident Investigation Lab.

## Phase 1 — Planning and Repository Setup

* [x] Create GitHub repository
* [x] Create initial repository structure
* [x] Define project scope
* [x] Define lab architecture and networking plan

## Phase 2 — Build the SIEM Environment

* [x] Create Ubuntu Splunk server VM
* [x] Install and configure Splunk Enterprise
* [x] Create Windows 11 endpoint VM
* [x] Install Splunk Universal Forwarder
* [x] Install and configure Sysmon
* [x] Enable Windows auditing and PowerShell logging
* [x] Configure isolated VirtualBox network
* [x] Verify connectivity between endpoint and Splunk

## Phase 3 — Configure and Validate Telemetry

* [x] Forward Windows Security logs
* [x] Forward Sysmon logs
* [x] Forward PowerShell logs
* [x] Forward Task Scheduler logs
* [x] Validate hosts, timestamps, and sourcetypes
* [x] Verify event ingestion and latency
* [x] Capture clean VM snapshots

## Phase 4 — Generate and Detect Suspicious Activity

* [x] Generate controlled authentication activity
* [x] Create and privilege a temporary local account
* [x] Execute harmless encoded PowerShell
* [x] Execute system-discovery commands
* [x] Create a benign scheduled task
* [x] Develop and validate SPL detections
* [x] Configure Splunk alerts
* [x] Document false positives and detection limitations

## Phase 5 — Detection Engineering and Visualization

* [ ] Create Sigma versions of selected detections
* [ ] Build SOC investigation dashboard
* [ ] Validate detections against generated activity
* [ ] Capture screenshots of searches, alerts, and dashboards

## Phase 6 — Incident Investigation and Containment

* [ ] Investigate authentication activity
* [ ] Investigate account and privilege changes
* [ ] Investigate PowerShell and process activity
* [ ] Investigate scheduled-task activity
* [ ] Reconstruct the incident timeline
* [ ] Map observed behavior to MITRE ATT&CK
* [ ] Remove the temporary account and scheduled task
* [ ] Verify containment in Splunk

## Phase 7 — Documentation and Portfolio Cleanup

* [ ] Complete incident report
* [ ] Add screenshots
* [ ] Review repository for sensitive information
* [ ] Update README with final results
* [ ] Mark project complete