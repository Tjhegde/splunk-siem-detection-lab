# Project Roadmap

This roadmap tracks the development of the Splunk SIEM Detection & Incident Investigation Lab.

## Phase 1 — Planning and Repository Setup

* [x] Create GitHub repository
* [x] Create initial repository structure
* [x] Define project scope
* [x] Define lab architecture and networking plan

## Phase 2 — Build the SIEM Environment

* [ ] Create Ubuntu Splunk server VM
* [ ] Install and configure Splunk Enterprise
* [ ] Create Windows 11 endpoint VM
* [ ] Install Splunk Universal Forwarder
* [ ] Install and configure Sysmon
* [ ] Enable Windows auditing and PowerShell logging
* [ ] Configure isolated VirtualBox network
* [ ] Verify connectivity between endpoint and Splunk

## Phase 3 — Configure and Validate Telemetry

* [ ] Forward Windows Security logs
* [ ] Forward Sysmon logs
* [ ] Forward PowerShell logs
* [ ] Forward Task Scheduler logs
* [ ] Validate hosts, timestamps, and sourcetypes
* [ ] Verify event ingestion and latency
* [ ] Capture clean VM snapshots

## Phase 4 — Generate and Detect Suspicious Activity

* [ ] Generate controlled authentication activity
* [ ] Create and privilege a temporary local account
* [ ] Execute harmless encoded PowerShell
* [ ] Execute system-discovery commands
* [ ] Create a benign scheduled task
* [ ] Develop and validate SPL detections
* [ ] Configure Splunk alerts
* [ ] Document false positives and detection limitations

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