# Project Roadmap

This document tracks the planned development of the Splunk SIEM Detection & Incident Investigation Lab.

The roadmap may change as the project develops.

## Phase 1 — Repository and Lab Planning

* [x] Create GitHub repository
* [x] Create initial repository structure
* [x] Document project scope
* [x] Document planned architecture
* [x] Create architecture diagram
* [x] Finalize lab IP-addressing scheme
* [x] Document host-resource allocation

## Phase 2 — Splunk Server

* [ ] Create Ubuntu virtual machine
* [ ] Update Ubuntu
* [ ] Install Splunk Enterprise
* [ ] Configure Splunk service
* [ ] Create Windows event index
* [ ] Configure Splunk receiving port
* [ ] Install Splunk Add-on for Microsoft Windows
* [ ] Validate Splunk Web access
* [ ] Document configuration

## Phase 3 — Windows Endpoint

* [ ] Create Windows 11 virtual machine
* [ ] Create lab-only administrator account
* [ ] Install operating-system updates
* [ ] Install Splunk Universal Forwarder
* [ ] Install or enable Sysmon
* [ ] Enable Windows auditing
* [ ] Enable PowerShell logging
* [ ] Enable Task Scheduler logging
* [ ] Configure Windows Event Log forwarding
* [ ] Document endpoint configuration

## Phase 4 — Network Isolation

* [ ] Create isolated VirtualBox internal network
* [ ] Configure static Splunk server address
* [ ] Configure static Windows endpoint address
* [ ] Verify endpoint-to-Splunk connectivity
* [ ] Verify Splunk receiving port connectivity
* [ ] Remove unnecessary Internet connectivity
* [ ] Verify lab isolation
* [ ] Capture clean VM snapshots

## Phase 5 — Data Ingestion

* [ ] Ingest Windows Security events
* [ ] Ingest Sysmon events
* [ ] Ingest PowerShell events
* [ ] Ingest Task Scheduler events
* [ ] Ingest Windows System events
* [ ] Ingest Windows Application events
* [ ] Validate hostnames
* [ ] Validate timestamps
* [ ] Validate sourcetypes
* [ ] Measure ingestion latency
* [ ] Document data sources

## Phase 6 — Controlled Incident Generation

* [ ] Generate failed authentication activity
* [ ] Generate successful authentication activity
* [ ] Create temporary local account
* [ ] Add temporary account to Administrators
* [ ] Execute harmless encoded PowerShell
* [ ] Execute system-discovery utilities
* [ ] Create benign scheduled task
* [ ] Confirm expected telemetry reaches Splunk
* [ ] Preserve investigation evidence

## Phase 7 — SPL Detection Engineering

* [ ] Create data-validation search
* [ ] Create failed-logon burst detection
* [ ] Create account-creation detection
* [ ] Create privileged-group membership detection
* [ ] Correlate account creation with administrator-group addition
* [ ] Create encoded PowerShell detection
* [ ] Create scheduled-task detection
* [ ] Create discovery-command burst detection
* [ ] Create ingestion-latency search
* [ ] Document expected false positives
* [ ] Document detection limitations

## Phase 8 — Alerting

* [ ] Convert validated searches into Splunk alerts
* [ ] Configure alert severity
* [ ] Configure scheduling
* [ ] Configure throttling
* [ ] Add analyst triage guidance
* [ ] Trigger alerts using controlled activity
* [ ] Capture sanitized alert evidence

## Phase 9 — Sigma Rules

* [ ] Write encoded PowerShell Sigma rule
* [ ] Write local Administrators membership Sigma rule
* [ ] Write scheduled-task Sigma rule
* [ ] Document required log sources
* [ ] Document required fields
* [ ] Document false positives
* [ ] Compare Sigma logic with corresponding SPL searches

## Phase 10 — SOC Dashboard

* [ ] Create investigation dashboard
* [ ] Add total-event visualization
* [ ] Add reporting-host visualization
* [ ] Add events-by-source visualization
* [ ] Add event-volume timeline
* [ ] Add failed-logon panel
* [ ] Add account-management panel
* [ ] Add PowerShell panel
* [ ] Add scheduled-task panel
* [ ] Add discovery-command panel
* [ ] Add ingestion-health panel
* [ ] Capture sanitized dashboard screenshots

## Phase 11 — Incident Investigation

* [ ] Identify initial suspicious activity
* [ ] Review failed authentication
* [ ] Identify subsequent successful authentication
* [ ] Investigate account creation
* [ ] Investigate administrator-group membership
* [ ] Investigate PowerShell execution
* [ ] Reconstruct process relationships
* [ ] Investigate discovery activity
* [ ] Investigate scheduled-task creation
* [ ] Build combined incident timeline
* [ ] Assess scope
* [ ] Document findings

## Phase 12 — MITRE ATT&CK Mapping

* [ ] Map account creation
* [ ] Map account manipulation
* [ ] Map PowerShell execution
* [ ] Map scheduled-task behavior
* [ ] Map user discovery
* [ ] Map system-information discovery
* [ ] Map network-configuration discovery
* [ ] Map process discovery
* [ ] Document limitations of ATT&CK mappings

## Phase 13 — Containment

* [ ] Preserve evidence
* [ ] Remove scheduled task
* [ ] Remove temporary account
* [ ] Verify containment on endpoint
* [ ] Verify containment activity in Splunk
* [ ] Document containment actions

## Phase 14 — Incident Report

* [ ] Write executive summary
* [ ] Document data sources
* [ ] Create UTC timeline
* [ ] Document technical findings
* [ ] Document ATT&CK mappings
* [ ] Document false positives
* [ ] Document detection limitations
* [ ] Document containment
* [ ] Document lessons learned
* [ ] Review report for sensitive information