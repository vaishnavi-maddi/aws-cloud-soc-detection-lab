# MITRE ATT&CK Mapping
This document maps implemented AWS CloudTrail detections to the MITRE ATT&CK framework to ensure coverage alignment with real-world adversary techniques.
The mapping demonstrates how cloud-native logging and detection mechanisms can identify high-risk IAM and infrastructure manipulation behaviors.
# Detection Coverage Matrix
| Detection Name                  | CloudTrail Event                          | MITRE Tactic                            | MITRE Technique                       | Technique ID | Rationale                                                            |
| ------------------------------- | ----------------------------------------- | --------------------------------------- | ------------------------------------- | ------------ | -------------------------------------------------------------------- |
| Access Key Creation             | CreateAccessKey                           | Persistence                             | Account Manipulation                  | T1098        | Attackers create API keys to maintain long-term programmatic access. |
| Administrator Policy Attachment | AttachUserPolicy (AdministratorAccess)    | Privilege Escalation                    | Exploitation for Privilege Escalation | T1068        | Privilege escalation through high-privilege IAM policy attachment.   |
| Root Account Usage              | userIdentity.type = Root                  | Privilege Escalation                    | Valid Accounts                        | T1078        | Root usage represents full administrative access.                    |
| EC2 Stop Event                  | StopInstances                             | Impact                                  | Service Stop                          | T1489        | Service disruption or operational interference.                      |
| EBS Snapshot Creation           | CreateSnapshot                            | Exfiltration                            | Transfer Data to Cloud Account        | T1537        | Snapshots may enable unauthorized data extraction.                   |
| Public Security Group Exposure  | AuthorizeSecurityGroupIngress (0.0.0.0/0) | Defense Evasion / Resource Modification | Modify Cloud Infrastructure           | T1578        | Weakens security posture by exposing infrastructure publicly.        |
| CloudTrail Tampering            | StopLogging / DeleteTrail                 | Defense Evasion                         | Impair Defenses                       | T1562        | Disabling logs prevents detection and investigation.                 |

# Summary
This lab demonstrates adversary-aligned detection engineering by mapping CloudTrail-based alerts to the MITRE ATT&CK framework. Each detection was validated through controlled simulation and verified via CloudWatch alarm activation and SNS notifications.
