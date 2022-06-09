# Infosec: Threat Modelling

## Resources
- [Wikipedia - Threat model](https://en.wikipedia.org/wiki/Threat_model)

## Steps
### 1. Create the design
Create a simple diagram showing how the nodes and flows connect

### 2. Apply Zones Of Trust
Designate Zones Of Trust for more critical areas:
- 0 = Not in control of system
- 1 = Boundary, external communication
- 2,3 = Low trust, data passes through
- 4,5 = Medium, business rules processing
- 6,7 = High, business critical processing
- 8,9 = Critical, data hits the disk

### 3. Apply STRIDE for Threats
Designate threats using Zone math to calculate STRIDE element.
- **S**poofing (target node) = ‘Not in control of system’ to any other
- **T**ampering (flow) = Less critical to more critical
- **R**epudiation (target node) = Spoofing +Tampering, or T+S
- **I**nformation Disclosure (flow) = More critical to less critical
- **D**enial of Service (target node, flow) = ‘Not in control of system’ to any other
- **E**levation Of Privilege (target node) = Less critical to more critical

### 4. Discover mitigations
Use STRIDE to OWASP Top 10 mapping to find mitigations.
- **S**poofing = A07:2021-Identification and Authentication Failures
- **T**ampering = A03:2021-Injection, A05:2021-Security Misconfiguration, A08:2021-Software and Data Integrity Failures
- **R**epudiation = A09:2021-Security Logging and Monitoring Failures
- **I**nformation Disclosure = A02:2021-Cryptographic Failures, A05:2021-Security Misconfiguration
- **D**enial-Of-Service = A02:2021-Cryptographic Failures, A05:2021-Security Misconfiguration, A06:2021-Vulnerable and Outdated Components
- **E**levation of Privilege = A01:2021-Broken Access Control, A05:2021-Security Misconfiguration, A06:2021-Vulnerable and Outdated Components, A10:2021-Server-Side Request Forgery

Each OT10 mitigation has an identifier, such as *A1.1* , which can be used to find the element in OWASP documentation. Apply relevant OT10 mitigations by identifier.
