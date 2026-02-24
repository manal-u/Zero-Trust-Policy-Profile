# 1. ZTA Component Definitions

## Policy Engine (PE)
The Policy Engine is the decision-making “brain” in Zero Trust. It collects security signals (who is requesting, how they authenticated, device health, network risk, etc.) and compares them against policy rules to decide whether to allow access, deny access, or require extra verification.

## Policy Administrator (PA)
The Policy Administrator is the component that turns the Policy Engine’s decision into a real access outcome. If the PE says “allow,” the PA can issue short-lived credentials or configure the access session. If the PE says “deny” or “step-up,” the PA triggers the required action (block access or require MFA).

## Policy Enforcement Point (PEP)
The Policy Enforcement Point is the “gatekeeper” that sits in front of the protected resource and enforces access. It intercepts the connection request and only allows traffic when it has valid authorization (like a token/session) that matches what the Policy Engine decided.

# 2. Core Principle Application

## Chosen Principle: Verify Explicitly
Verify Explicitly means access decisions are based on current, real security evidence, not on where a user is “supposed” to be (like being on an internal network). The Policy Engine enforces this by checking multiple signals each time access is requested.

### Example: Protecting the HR Employee PII Database
An HR specialist requests access to the HR Employee PII Database that includes background checks and certification status.

Before approving access, the Policy Engine verifies:
- **User identity assurance:** The user is in the HR group, account is active, and MFA was successfully completed.
- **Device posture:** The laptop is company-managed, encrypted, has EDR running, and meets patch requirements.
- **Network context:** The request comes from the corporate network or corporate VPN and is not from an anonymous/proxy network.

If all signals meet policy, the Policy Engine returns an allow decision and can include constraints like a time-limited session token. If any signal fails (example: user is valid but device is unmanaged), the Policy Engine denies access or requires step-up verification.

# 3. Simplified Policy Table

| Policy Requirement (Signal) | Condition to be Met by User | Action if Condition is Met |
|---|---|---|
| User Identity | User is an active employee in the HR role group AND uses MFA AND account risk is not flagged. | Grant Access |
| Device Posture | Device is facility-managed, disk encrypted, EDR enabled, and OS patches meet baseline requirements. | Grant Access |
| Network Context | Request originates from corporate network or corporate VPN AND from an approved geo-region AND not from anonymous/proxy networks. | Grant Access |

# 4. Submission Details

# Git Repository Metadata

Project: Lab 6 - Zero Trust Policy  
Filename: ZT-Policy-Profile.md  
Commit Message: Add Zero Trust policy profile for HR PII database
Due Date: March 2, 2026
