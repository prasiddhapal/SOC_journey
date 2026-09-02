**Day 38 | Linux Authentication & Incident Reconstruction**  
**Platform:** Hack The Box Sherlocks  
   
 **Challenge:** Brutus  
   
 **Category:** DFIR  
   
 **Difficulty:** Easy  
   
 **Status:** Solved  
**Objective**  
Investigate a Linux/Confluence server compromise using auth.log and wtmp, reconstruct the attack timeline, identify persistence, map the behavior to MITRE ATT&CK, and recover the final privileged command.  
**Artifacts**  
- auth.log - SSH authentication, PAM, account-management and sudo events.  
- wtmp - Binary login/session history.  
- utmp.py - Python parser for wtmp.  
**Investigation Flow**  
1. Identify the brute-force source.  
2. Confirm the compromised account.  
3. Correlate auth.log with wtmp.  
4. Identify the attacker's session number.  
5. Detect creation of a privileged persistence account.  
6. Map persistence to ATT&CK.  
7. Reconstruct session termination.  
8. Identify the final privileged download command.  
**Key Finding**  
The attack chain was: SSH brute force -> successful root access -> interactive session -> creation of cyberjunkie -> sudo privilege assignment -> privileged external script download.  
**SOC Relevance**  
The exercise demonstrates why authentication, session, account-management and sudo artifacts must be correlated into one timeline rather than investigated as isolated alerts.  
