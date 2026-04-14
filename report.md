# SOC Phishing Incident Response Lab
Simulated phishing attack investigation using Splunk SIEM and MITRE ATT&CK framework.



## What I Observed

The incident began with a phishing email sent to user "jsmith" from a suspicious domain impersonating Microsoft ("micr0soft-secure.com"). The email contained a malicious link, which the user clicked shortly after receiving it.

Following the link click, the user entered their credentials into a fraudulent login page, indicating a successful credential harvesting attack.

Shortly after, a successful login attempt was recorded from an IP address located in Russia (185.220.101.45), which is inconsistent with normal user behavior and indicates unauthorized access.

Once access was obtained, multiple sensitive files were accessed, including employee_records.xlsx and finance_data.xlsx. A large download of employee data was also observed, suggesting potential data exfiltration.

An anomaly detection alert ("impossible_travel") was triggered, indicating that the system identified the login behavior as suspicious. The session was subsequently terminated by the SOC team, effectively stopping the attack.


## MITRE ATT&CK Mapping

					| Stage | Log Event | MITRE Technique |
					|------|----------|----------------|
| Initial Access | email_received/email_clicked | Phishing (T1566) |
| Credential Access | credential_entered | Credentials from User (T1056) |
| Persistence / Access | login_attempt (Russia IP) | Valid Accounts (T1078) |
| Discovery / Collection | file_access | Data from Local System (T1005) |
| Exfiltration | download (45MB) | Exfiltration Over Web Services (T1567) |
| Detection | login_detected_anomaly | Anomalous Behavior Detection |
| Response | session_terminated | Incident Response Action |


## Incident Summary

On April 14, 2026, a phishing attack resulted in the compromise of user "jsmith’s" credentials. The attack originated from a spoofed email impersonating a legitimate service, which successfully tricked the user into clicking a malicious link and submitting login credentials.

The attacker leveraged these valid credentials to gain unauthorized access from a foreign IP address, bypassing traditional authentication controls. Following access, the attacker navigated the system and accessed sensitive organizational data, including employee and financial records.

A significant data transfer (45MB) was observed, indicating likely data exfiltration. The activity triggered an "impossible travel" alert, which led to detection by the Security Operations Center.

The SOC responded by terminating the session, effectively containing the incident. This attack highlights the risks associated with credential-based attacks and reinforces the need for phishing awareness and anomaly-based detection mechanisms.


## Key Takeaways

- Phishing remains an effective initial access vector when users are not able to identify spoofed domains.
- Credential-based attacks can bypass traditional defenses when valid accounts are used.
- Monitoring for anomalous behavior, such as impossible travel, is critical for early detection.
- Rapid SOC response can significantly reduce the impact of data exfiltration incidents.