# AWS Cloud Threat Detection & Response Lab
This project demonstrates the design and implementation of a cloud-native threat detection pipeline in AWS using:
- AWS CloudTrail
- Amazon CloudWatch Logs
- CloudWatch Metric Filters
- CloudWatch Alarms
- Amazon SNS
The lab simulates common cloud attack behaviors and implements automated detection aligned with the MITRE ATT&CK framework.
# Architecture
CloudTrail --> CloudWatch Logs --> Metric Filters --> Alarms --> SNS Email Alerts 
All API activities are logged via CloudTrail and evaluated in near real-time using custom detection rules.
# Simulated Attack Scenarios
The following behaviors were intentionally simulated:
- IAM user creation
- AdministratorAccess policy attachment (Privilege Escalation)
- Programmatic access key generation (Persistence)
- EC2 instance stop (Operational Impact)
- EBS snapshot creation (Data Exfiltration Preparation)
- Public security group exposure (0.0.0.0/0)
- Root account usage
- CloudTrail tampering attempts (StopLogging/DeleteTrail)
# Detection Use Cases Implemented
| Detection              | CloudTrail Event                       |
| ---------------------- | -------------------------------------- |
| Privilege Escalation   | AttachUserPolicy (AdministratorAccess) |
| Access Key Persistence | CreateAccessKey                        |
| Instance Disruption    | StopInstances                          |
| Snapshot Creation      | CreateSnapshot                         |
| Public Exposure        | AuthorizeSecurityGroupIngress          |
| Root Usage             | userIdentity.type = Root               |
| Log Tampering          | StopLogging / DeleteTrail              |

# MITRE ATT&CK Mapping
This detection pipeline aligns with the following MITRE techniques:
- T1078 – Valid Accounts
- T1098 – Account Manipulation
- T1068 – Privilege Escalation
- T1489 – Service Stop
- T1537 – Transfer Data to Cloud Account
- T1562 – Impair Defenses
# Incident Response Workflow
Detection --> Triage --> Log Correlation --> Containment --> Remediation --> Hardening
