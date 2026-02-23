This document outlines the detection logic implemented using AWS CloudTrail, CloudWatch Logs, metric filters, and alarms.
# 1. Privilege Escalation Detection
Event: AttachUserPolicy
Condition: AdministratorAccess policy attached
Risk: Unauthorized elevation of IAM permissions
Detection Mechanism: CloudWatch metric filter + alarm

# 2. Persistence via Access Key Creation
Event: CreateAccessKey
Risk: Long-term API access persistence
Detection Mechanism: CloudWatch metric filter + alarm

# 3. Root Account Activity Monitoring
Condition: userIdentity.type = Root
Risk: Highest level account usage
Detection Mechanism: Metric filter + SNS alert

# 4. EC2 Service Disruption
Event: StopInstances
Risk: Business impact / service disruption
Detection Mechanism: Alarm triggered upon API call

# 5. Snapshot Creation Monitoring
Event: CreateSnapshot
Risk: Potential data exfiltration preparation
Detection Mechanism: CloudWatch log pattern detection

# 6. Security Group Public Exposure
Event: AuthorizeSecurityGroupIngress
Condition: 0.0.0.0/0 detected
Risk: Infrastructure exposure to public internet
Detection Mechanism: Metric filter + alarm

# 7. CloudTrail Tampering Detection
Events: StopLogging, DeleteTrail
Risk: Log disablement and defense evasion
Detection Mechanism: High-priority alarm

# Detection Workflow
CloudTrail → CloudWatch Log Group → Metric Filter → CloudWatch Alarm → SNS Email Notification. 

All detections were validated via simulated attack behavior and confirmed through alarm state transition to "ALARM".
