
# Fraud Detection Using Logs

## Example 1: Account Takeover Leading to Financial Fraud

Scenario:
An attacker gains access to a legitimate user account and performs unauthorized financial activity.

Logs Used:
- Application authentication logs
- User activity logs
- Transaction logs

Timeline:
09:12 – Multiple failed login attempts
09:13 – Successful login from a new geographic location
09:14 – Password changed
09:16 – High-value transaction initiated

Detection Techniques:
- Timestamp correlation
- Anomaly detection

SOC Response:
- Block transaction
- Lock user account
- Force password reset


## Example 2: Credit Card / Payment Testing Fraud

Scenario:
An attacker tests stolen payment card details using multiple small transactions before executing a large payment.

Logs Used:
- Payment gateway logs
- Application transaction logs
- API access logs

Timeline:
14:01 – Transaction failed (small amount)
14:02 – Transaction failed
14:03 – Transaction failed
14:04 – High-value transaction successful

Detection Techniques:
- Timestamp correlation
- Anomaly detection

SOC Response:
- Reverse transaction
- Flag payment method
- Notify fraud investigation team