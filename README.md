# Event ID 77 - Detected Suspicious XLS File 📄


## Short Overview of the Investigation 🔬

This investigation covers a medium-severity malware alert from LetsDefend's SOC138 detection rule. A suspicious macro-enabled Excel file was detected on the endpoint Sofia. The investigation focused on validating the file, reviewing network activity, checking its quarantine status, and determining the appropriate response.

*Investigation verdict*: True Positive - Malicious file, not quarantined.


## Alert Summary and Timeline ⌛

### Alert Summary

| Field | Details |
| ----- | ------- |
| Platform | LetsDefend |
| Event ID | 77 |
| Rule | SOC138: Detected Suspicious XLS File |
| Severity | Medium |
| Event Time | March 13, 2021, 20:20 |
| Hostname | Sofia |
| Source IP | 172.16.17.56 |
| File Name | ORDER SHEET & SPEC.xlsm | 
| MD5 | 7ccf88c0bbe3b29bf19d877c4596a8d4 |
| Device Action | Allowed |
| MITRE ATT&CK | T1112 - Modify Registry |

### Timeline

- *20:20*: LetsDefend generated an alert for a suspicious Excel file.
- *Investigation*: The file hash and available malware analysis results were reviewed.
- *Log analysis*: Endpoint and network logs were checked for suspicious execution and communication with external infrastructure.
- *Final assessment*: The file was malicious and had not been quarantined.


## Investigation Steps 🕵️‍♂️

1. ### Alert Triage
I reviewed the alert details, affected endpoint, suspicious filename, file hash, severity, and device action. The Allowed status indicated that the file had not been blocked by the security control.

2. ### Malware Analysis
I then checked the file hash using threat intelligence resources, including VirusTotal. The available results identified the file as malicious. Further analysis indicated suspicious macro and encoded PowerShell activity associated with downloading and executing a payload.

3. ### Endpoint and Network Investigation
I reviewed endpoint and network logs for suspicious PowerShell activity and potential communication with attacker-controlled infrastructure. The investigation identified the external IP 177.53.143.89 as a relevant command-and-control indicator and found evidence of communication with that address.

4. ### Quarantine Status
The device action was Allowed, meaning the malware was not quarantined or blocked. I initially selected “Quarantined” in the playbook, which was incorrect. The evidence supports selecting “Not Quarantined.”


## My Findings, Conclusions, and Recommended Response 💁‍♀️

### Findings

- The suspicious Excel file was identified as malicious.
- The endpoint security action was Allowed.
- Suspicious encoded PowerShell activity was associated with the incident.
- Network investigation identified communication with a relevant external IP.
- The malware was not quarantined.

### Conclusion

This is a True Positive malware incident. The malicious file was allowed, and the investigation indicated potential endpoint compromise. The affected device should not be considered clean without further investigation and remediation.

### Recommended Response

1. Isolate the affected endpoint to limit further malicious activity.
2. Remove or quarantine the malicious file using the appropriate security controls.
3. Investigate PowerShell execution, registry modifications, and possible persistence.
4. Search for communication with the identified external IP and related indicators.
5. Preserve relevant logs and document containment and remediation actions.
6. Verify that the endpoint is clean before returning it to normal operation.


## Screenshots 📷

<img width="710" height="290" alt="Screenshot 2026-10-13 153333" src="https://github.com/user-attachments/assets/ff352114-5baa-49f1-bb64-01d56c5ff89d" />

<img width="704" height="259" alt="Screenshot 2026-10-13 153345" src="https://github.com/user-attachments/assets/4ca430b5-7c7a-4523-acc1-d761b9e3f0f4" />


## Lessons Learned ✍️

- A file marked Allowed is not quarantined. Always verify the actual security action before answering the playbook.
- *Validate with evidence*: File reputation, endpoint telemetry, and network logs help establish whether an alert is a true positive.
- *Investigate potential compromise*: Malicious execution and external communication require further investigation and containment.
- *Accuracy matters*: I achieved a 67% playbook score and incorrectly marked the malware as quarantined. This highlighted the importance of carefully checking device actions and ensuring playbook answers match the investigation evidence.
