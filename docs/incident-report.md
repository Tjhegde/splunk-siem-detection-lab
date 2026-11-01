# Incident Report — Simulated Windows Account Compromise

**Incident type:** Controlled security simulation (not an actual account compromise)  
**Affected system:** WIN11-ENDPOINT (Windows 11)  
**SIEM:** Splunk Enterprise  
**Investigation date:** October 31, 2026  
**Observed event period:** October 31, 2026, 20:31:04–23:34:39 UTC  
**Status:** Contained and Verified. Test account removed, administrator membership cleared, and scheduled task confirmed absent.

## 1. Executive Summary

A controlled security scenario was performed on an isolated Windows 11 virtual machine to evaluate Windows event collection, Splunk SPL detections, scheduled alerting, and incident investigation.

The scenario involved local account creation, repeated authentication failures, successful logons, administrator-group membership changes, encoded PowerShell execution, system-discovery commands, and scheduled-task registration.

Windows Security, PowerShell Operational, and Task Scheduler Operational events were forwarded to Splunk Enterprise using the Universal Forwarder.

The broad investigation search identified **1,593 Windows events across nine selected event IDs**. A focused investigation query correlated **35 relevant events** associated with the simulated activity.

This was an authorized simulation using harmless commands. No malware was used, and no real compromise was identified.

## 2. Investigation Scope

| Component | Details |
|---|---|
| Endpoint | WIN11-ENDPOINT — 10.10.20.20 |
| SIEM server | SPLUNK-SERVER — 10.10.20.10 |
| Splunk index | `windows` |
| Relevant logs | Windows Security, PowerShell Operational, Task Scheduler Operational |
| Process telemetry | Security Event ID 4688 |
| Test account | `siem-p4-test` |
| Test scheduled task | `SIEM-Phase4-Test` |
| Event format | Raw Windows XML |

Windows events were analyzed using SPL field extraction without the Splunk Add-on for Microsoft Windows.

### Broad Event Summary

The following counts were obtained from the broad event-count search. They include routine Windows activity and are not limited to the test account.

| Event ID | Description | Count |
|---|---|---:|
| 106 | Scheduled task registration | 5 |
| 4104 | PowerShell script-block logging | 195 |
| 4624 | Successful logon | 66 |
| 4625 | Failed logon | 8 |
| 4688 | Process creation | 1,312 |
| 4720 | Account creation | 2 |
| 4726 | Account deletion | 1 |
| 4732 | Local group membership addition | 2 |
| 4733 | Local group membership removal | 2 |
| **Total** | | **1,593** |

The focused incident timeline contained 35 events: 1 account creation, 19 selected process executions, 5 successful logons, 7 failed logons, 2 administrator-group additions, and 1 matching scheduled-task registration.

## 3. Investigation Timeline

The following timeline summarizes the observed activity on October 31, 2026. All timestamps are UTC.

| Timestamp (UTC) | Event ID | Observed activity |
|---|---|---|
| 20:45:49 | 4720 | Local test account `siem-p4-test` created |
| 20:50:31 | 4688 | `whoami.exe` executed |
| 20:52:21 | 4688 | `net.exe user siem-p4-test *` observed, consistent with account password management |
| 20:53:59–20:59:41 | 4624 | Five successful logons for `siem-p4-test` |
| 20:56:09–21:11:26 | 4625 | Seven failed logons for `siem-p4-test` |
| 21:01:06 | 4732 | Account added to the built-in Administrators group |
| 21:03:31 | 106 | Scheduled-task registration matching `SIEM-Phase4-Test` |
| 21:19:48 | 4733 | Administrator-group membership removal |
| 21:19:51 | 4732 | Another addition to the Administrators group |
| 21:21:15 | 4688 | Encoded PowerShell execution |
| 21:24:54 | 4688 | Additional encoded PowerShell execution |
| 21:27:58 | 4688 | Additional encoded PowerShell execution |
| 23:28:29 | 4733 | Administrator-group membership removal |
| 23:28:42 | 4726 | Test account `siem-p4-test` deleted |

Successful logons occurred before and during the failed-logon testing period. The available evidence does not establish that a successful logon resulted from password guessing.

## 4. Detection Results

Three SPL detections were implemented, tested, and configured as scheduled Splunk alerts.

| Detection | Data source | Investigation result |
|---|---|---|
| Repeated Failed Logons | Security 4625 | **Triggered — Medium.** Seven focused failed logons exceeded the threshold of three failures within two hours. |
| Local Admin Membership Change | Security 4732 | **Triggered — High.** Two additions to the built-in Administrators group were detected. |
| Encoded PowerShell Execution | Security 4688 | **Triggered — Medium.** Multiple PowerShell processes launched with `-EncodedCommand` were detected. |

All three alerts were confirmed in Splunk's Triggered Alerts interface.

These events represent behaviors that warrant investigation, not independent proof of malicious activity.

## 5. MITRE ATT&CK Mapping

The following techniques correspond to behaviors represented by the controlled simulation.

| Behavior | MITRE ATT&CK Technique |
|---|---|
| Local account creation | T1136.001 — Create Account: Local Account |
| Administrator-group membership addition | T1098.007 — Account Manipulation: Additional Local or Domain Groups |
| PowerShell execution | T1059.001 — Command and Scripting Interpreter: PowerShell |
| Current-user discovery (`whoami`) | T1033 — System Owner/User Discovery |
| Local account enumeration | T1087.001 — Account Discovery: Local Account |
| Process discovery (`tasklist`) | T1057 — Process Discovery |
| Scheduled-task creation | T1053.005 — Scheduled Task/Job: Scheduled Task |

The process discovery and local account enumeration mappings apply where those specific actions are supported by the underlying command-line records.

These mappings describe the simulated techniques and do not imply an actual intrusion.

## 6. Containment and Verification

After completing the simulated activity, account and privilege cleanup operations were investigated.

| Action | Verification result |
|---|---|
| Remove administrator-group membership | **Logged.** Event ID 4733 appeared twice, at 21:19:48 and 23:28:29 UTC. The member SID matched the SID shown in the group-addition evidence. |
| Delete temporary test account | **Logged.** Event ID 4726 recorded deletion of `siem-p4-test` at 23:28:42 UTC. |
| Remove `SIEM-Phase4-Test` scheduled task | **Verified.** No matching registered task found during endpoint inspection. |
| Verify account, group, and task state on Windows | **Verified.** Test account, administrator membership, and scheduled task absent. |

**Containment outcome:** Windows Security logs confirmed the deletion of the temporary test account and recorded the removal of administrator-group memberships. Additional endpoint verification confirmed that `siem-p4-test` no longer existed, was absent from the local Administrators group, and that the `SIEM-Phase4-Test` scheduled task was no longer registered. All simulated incident cleanup checks were successfully completed.

## 7. Limitations and False Positives

- Failed authentication attempts can result from legitimate password mistakes, expired credentials, or account troubleshooting.
- Administrator-group changes can occur during authorized system maintenance.
- Encoded PowerShell is not inherently malicious and may be used by legitimate administrative automation.
- Windows Security Event ID 4688 confirms process creation but does not necessarily prove that every command completed successfully.
- The broad event counts include routine Windows activity and should not be interpreted as 1,593 malicious or simulated incident events.
- PowerShell Event ID 4104 indicates script-block logging; not every such event represents suspicious execution.
- Detection effectiveness depends on audit policies, available event fields, event forwarding, and retention.
- Sysmon Event ID 1 was not available for the tested PowerShell activity, so process monitoring relied on Security Event ID 4688.
- The lab involved a single Windows endpoint and Splunk server and does not establish enterprise-wide detection coverage.

## 8. Lessons Learned

This exercise provided hands-on experience with:

- Collecting and validating Windows security telemetry in Splunk Enterprise.
- Writing SPL searches against raw Windows event XML.
- Configuring and validating scheduled security alerts.
- Correlating authentication, account management, process execution, and scheduled-task events.
- Reconstructing chronological incident timelines from multiple Windows log sources.
- Distinguishing broad event collection from focused security investigation.
- Mapping observed behavior to MITRE ATT&CK.
- Investigating cleanup activity and understanding the limits of event-based verification.

An important troubleshooting lesson involved adapting detection logic to the available telemetry. The original PowerShell detection expected Sysmon Event ID 1, but Windows Security Event ID 4688 provided the process information needed to identify encoded PowerShell execution successfully.

The investigation also demonstrated the importance of distinguishing observed evidence from assumptions. Authentication failures alone do not establish a successful brute-force attack, and Windows event logs recording cleanup actions do not necessarily confirm the final state of a system. For this reason, additional endpoint checks were performed to verify that the temporary account, administrator-group membership, and scheduled task had been removed.

**Conclusion:**

The simulated security investigation successfully demonstrated Windows event collection, detection engineering, alert validation, and incident investigation using Splunk Enterprise. All three scheduled detection alerts—repeated failed logons, local administrator-group additions, and encoded PowerShell execution—were successfully triggered and verified.

The investigation analyzed 1,593 Windows events across nine selected event IDs, with a focused timeline of 35 events associated with the simulated activity. Correlating authentication records, account management events, process creation logs, and scheduled-task telemetry enabled the reconstruction of the activity performed on the Windows 11 endpoint.

Windows Security logs confirmed the deletion of the temporary test account and recorded administrator-group membership removals. Additional endpoint checks verified that the test account, elevated group membership, and scheduled task were no longer present.

The exercise provided practical experience in identifying suspicious behaviors, troubleshooting detection gaps, reconstructing security events, and validating cleanup procedures. All activity was conducted within an isolated lab environment, and no actual compromise occurred.