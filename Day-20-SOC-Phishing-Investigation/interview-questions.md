# Day 20 - SOC Interview Questions

## Technical Questions

### 1. What is phishing?

**Answer:**

Phishing is a social-engineering attack where an attacker uses a fraudulent email, message, link, or website to trick a user into performing an unsafe action. The goal may be to steal credentials, deliver malware, or redirect the victim to malicious infrastructure.

In our Day 20 investigation, the attacker used a fake Windows 11 Pro upgrade as the lure. The email directed the recipient to `windows-update.site`, which displayed a fake Windows upgrade page and suspicious verification instructions.

---

### 2. What made the email suspicious?

**Answer:**

Several indicators made the email suspicious. The sender used `update@windows-update.site`, which attempts to look like a legitimate Windows update service. The subject promised a free Windows 11 Pro upgrade, creating an attractive lure for the recipient.

The landing page also used fake Windows branding and suspicious instructions involving `Win + R`, `Ctrl + V`, and `Enter`. These indicators together made the email highly suspicious and required further investigation.

---

### 3. How would you investigate a phishing email?

**Answer:**

I would begin by analyzing the sender address, sender domain, subject, recipient, email headers, URLs, and attachments. I would then check whether the domain, IP address, URL, or file hash has a suspicious reputation using available threat-intelligence sources.

After that, I would correlate the email with proxy, DNS, authentication, and endpoint logs. I would determine whether the user accessed the URL, downloaded anything, executed a process, or submitted credentials. Finally, I would classify the alert, assign severity, document the evidence, and recommend containment.

---

### 4. What is an IOC?

**Answer:**

IOC stands for **Indicator of Compromise**. It is a piece of evidence that can help identify or investigate potentially malicious activity.

Common IOCs include IP addresses, domains, URLs, email addresses, file hashes, filenames, and suspicious processes. In our investigation, examples included `windows-update.site`, the phishing URL, the sender IP, and the suspicious sender address.

However, an IOC should be interpreted in context. An IP address or domain alone does not automatically prove that a system is compromised.

---

### 5. Why doesn't accessing a malicious URL automatically mean the endpoint is compromised?

**Answer:**

Accessing a malicious URL confirms that the user or browser interacted with suspicious infrastructure, but it does not prove that malware was downloaded or executed.

For example, after detecting access to `windows-update.site`, I would investigate endpoint telemetry for browser downloads, child processes, PowerShell, command execution, persistence, or other suspicious activity.

In our Day 20 investigation, the URL access was confirmed, but malware execution and full endpoint compromise could not be confirmed because sufficient endpoint telemetry was unavailable.

---

### 6. What would you do after confirming a phishing attack?

**Answer:**

First, I would contain the threat by quarantining the phishing email and blocking the confirmed malicious domain or infrastructure. I would then determine whether other users received the same email and identify any additional affected endpoints.

Next, I would investigate whether the user clicked the link, downloaded a file, executed a payload, or submitted credentials. If credentials were exposed, I would reset them and review related authentication activity.

Finally, I would document the incident, record the IOCs, determine the severity, and continue monitoring for related activity.

---

### 7. Why is evidence correlation important in SOC investigations?

**Answer:**

A single log event usually does not provide enough context to determine whether an activity is malicious. Correlation allows an analyst to connect different sources such as email logs, proxy logs, DNS activity, authentication events, and endpoint telemetry.

For example, an email containing a suspicious URL is one indicator. If the same URL is then accessed by a user's browser and followed by a suspicious process execution, the evidence becomes much stronger.

Correlation helps the analyst build an accurate timeline, determine the scope of an incident, and avoid making unsupported conclusions.

---

# HR Questions

### 8. Why do you want to become a SOC Analyst?

**Answer:**

I want to become a SOC Analyst because I enjoy investigating security events and solving problems using evidence. I am particularly interested in understanding how attacks happen, how they can be detected, and how analysts respond to them.

I have been building my practical foundation through Linux investigation, authentication analysis, process investigation, network analysis, and now hands-on SOC alert investigation. My goal is to continue developing these skills with SIEM, endpoint security, threat intelligence, and incident response.

---

### 9. How do you handle an unfamiliar security alert?

**Answer:**

I would not immediately assume that the alert is malicious. First, I would understand what triggered the alert and identify the affected user, host, source, destination, and timeframe.

Then I would collect relevant evidence and investigate the activity using available logs and security tools. If I cannot determine the answer, I would document what I have found and escalate the alert with the relevant evidence rather than making an unsupported decision.

My approach is to stay methodical and evidence-driven, especially when dealing with incomplete information.

---

### 10. What is your biggest strength as a cybersecurity learner?

**Answer:**

My biggest strength is analytical thinking and my willingness to learn through hands-on practice. I try to understand the reason behind an alert or command rather than simply memorizing the syntax.

For example, during the Day 20 phishing investigation, I learned to distinguish between confirmed URL access and unconfirmed endpoint compromise. That helped me understand why a SOC analyst must separate observed evidence from assumptions before assigning severity or recommending containment.
