# Simulated Attack Scenario

1. Attacker performs brute force attack on user accounts
2. Eventually gains access to one account
3. Logs in successfully from a new IP
4. Escalates privileges
5. Moves laterally across systems

---

## Expected Detections

- Spike in failed logins (4625)
- Suspicious successful login (SigninLogs)
- Privilege escalation event (4672)
- Increased internal connections (4624)
