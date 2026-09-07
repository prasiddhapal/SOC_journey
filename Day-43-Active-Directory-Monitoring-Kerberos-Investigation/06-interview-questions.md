# 06 | Interview Questions

Q: What does 4768 represent?
A: Kerberos authentication-service/TGT request.

Q: What does 4769 represent?
A: Kerberos service-ticket/TGS request.

Q: Why is Type 3 common?
A: Network activity such as file-share access and remote administration creates many network logons.

Q: Why baseline AD activity?
A: Normal enterprise environments generate large volumes of authentication events, so anomaly detection requires expected behavior.

Q: Why correlate account creation with first TGT?
A: It validates onboarding activity and provides source-host context for the new identity.
