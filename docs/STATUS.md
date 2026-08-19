# Project Status

**Status:** In Progress

**Current Stage:** Initial repository setup and lab planning

This file provides a concise snapshot of the project's current state. The more detailed implementation plan is available in [`ROADMAP.md`](ROADMAP.md).

## Completed

* [x] Defined the overall SIEM lab concept
* [x] Selected Splunk as the primary SIEM platform
* [x] Planned a two-VM Splunk/Windows architecture
* [x] Defined the controlled incident scenario
* [x] Identified planned telemetry sources
* [x] Identified planned detection categories
* [x] Created the GitHub repository
* [x] Created the initial repository structure
* [x] Added initial project documentation

## Currently Working On

* [ ] Building the virtual lab environment
* [ ] Preparing the Splunk server
* [ ] Preparing the Windows endpoint
* [ ] Creating the initial architecture diagram

## Up Next

* Configure Splunk Enterprise
* Configure the Splunk receiving port
* Install Splunk Universal Forwarder on Windows
* Configure Windows event collection
* Configure Sysmon
* Validate event ingestion into Splunk

## Not Yet Started

Detection engineering, alerting, dashboard creation, incident investigation, Sigma rules, ATT&CK mapping, containment, and the final incident report have not yet been completed.

Documentation in this repository will be updated as those stages are reached.

## Repository Principle

This repository is intended to reflect the actual development of the lab.

Items will only be marked as complete after they have been implemented and validated. Planned functionality will remain clearly labeled as planned or in progress rather than being presented as completed work.

## Last Major Milestone

Initial repository and documentation structure created.
