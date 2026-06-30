# aws-security-monitoring-sandbox
# AWS Secure Infrastructure & Incident Monitoring Sandbox

## 📌 Project Overview
This repository contains the architecture blueprint and implementation documentation for a secure, isolated three-tier cloud environment built entirely within the AWS Free Tier. The goal of this project is to apply core defensive cybersecurity principles—such as network isolation, the principle of least privilege, and automated continuous monitoring—to protect cloud workloads against unauthorized access.

---

## 🏗️ Architecture Diagram
```text
[Internet] ---> [AWS Internet Gateway] 
                       │
                       ▼
          [Public Subnet: NAT Gateway] 
                       │
                       ▼
          [Private Subnet: EC2 Server] <--- [Strict Stateful Security Group]
                       │
                       ▼
          [AWS CloudTrail / CloudWatch Logs] (Centralized Threat Audit Trail)
                       │
                       ▼
          [Amazon SNS Alerting System] ---> (Instant Security Team Email Alert)
```

---

## 🔒 Implemented Security Controls

### 1. Network Hardening (VPC & Subnets)
* **Custom Topology:** Deployed a dedicated Virtual Private Cloud (VPC) rather than relying on default configurations to ensure absolute network baseline control.
* **Workload Isolation:** Placed the virtual target server (`EC2`) entirely within a private subnet with no assigned public IP address, removing it completely from public internet scans.

### 2. Perimeter Defense & Least Privilege (Security Groups & IAM)
* **Zero-Trust Firewalling:** Configured custom EC2 Security Groups to drop 100% of inbound connections by default, mitigating brute-force vectors.
* **Identity Management:** Hardened root authentication with Multi-Factor Authentication (MFA) and structured permission templates to strictly isolate administrative duties from auditing functions.

### 3. Threat Detection & Automated Alerting (CloudTrail, CloudWatch, SNS)
* **Immutable Audit Trails:** Enabled **AWS CloudTrail** globally to intercept and record every programmatic action and API call across the infrastructure.
* **Real-Time Signature Matching:** Deployed custom JSON metric filters into **AWS CloudWatch Logs** to monitor for critical unauthorized adjustments:
  ```json
  { (.eventName = AuthorizeSecurityGroupIngress) || (.eventName = RevokeSecurityGroupIngress) }
  ```
* **Incident Alerting:** Tied the metric filters directly to an **Amazon SNS (Simple Notification Service)** topic, spinning up automated, instantaneous email dispatches to the response team the moment a firewall alteration is attempted.

---

## 🚀 Key Takeaways & Skills Learned
* **Cloud Infrastructure:** VPC design, subnetting, internet gateways, routing logic, and virtual machine deployment.
* **Defensive Operations:** Log streaming, pattern matching, metric aggregation, and event-driven alerting rules.
* **Security Frameworks:** Practiced the implementation of **NIST SP 800-53** controls surrounding Access Control (AC) and Audit & Accountability (AU).

---

## 📧 Connect With Me
I actively document my cloud cybersecurity journey. Check out my thoughts and project updates on [My LinkedIn Profile]](https://www.linkedin.com/in/makobeng-mampana-78a256a5/)!
