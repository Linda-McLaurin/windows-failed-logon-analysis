# Windows Failed Logon Analysis

SOC Analyst portfolio project focused on manual analysis of Windows Security Event logs (Event ID 4625) to detect failed logon and brute-force activity.

## Project Objective
Analyze a sample of Windows Security Event ID 4625 (Failed Logon) records, identify malicious activity, map it to the MITRE ATT&CK framework, and document findings in a professional SOC format.

## Method
- Manual log analysis (no automated tools or scripts used)
- Identification of source IPs, targeted accounts, and Logon Types
- Differentiation between remote (network) and local (interactive) failures
- MITRE ATT&CK mapping

## Sample Log
The file `sample-4625-events.log` contains realistic Windows failed logon events, including both external attack activity and low-risk internal failures.

## Findings

**Alert Title:** Possible Windows Brute-Force / Password Guessing Attack

**Source IP:** 203.0.113.88

**Target:** Windows host (Security Event ID 4625)

**Time Window:** 2026-07-28 09:14:22 – 09:22:14

**Activity Summary:**  
The source IP 203.0.113.88 performed 10 failed logon attempts (Event ID 4625) against a Windows host within an 8-minute window. All attempts used Logon Type 3 (Network). The attacker primarily targeted the Administrator account (7 attempts) and also tried the usernames admin and guest. No successful authentication from this IP was observed in the log.

**Key Observations:**
- Total failed attempts from this IP: 10
- Most targeted account: Administrator (7 times)
- Other accounts tried: admin (2), guest (1)
- Logon Type: 3 (Network)
- Other IPs in the log appear low-risk (one external single attempt and one internal interactive failure)

**MITRE ATT&CK:**
- Tactic: Credential Access
- Technique: T1110 – Brute Force
- Sub-technique: T1110.001 – Password Guessing

**Recommended Actions:**
- Block the IP 203.0.113.88 at the firewall / perimeter
- Review and enforce account lockout policies
- Confirm there were no successful logons from this IP
- Monitor for similar activity from other external IPs
- Consider restricting network logons for privileged accounts where possible

**Analyst Notes:**  
The activity is consistent with automated password guessing against common administrative account names. The presence of Logon Type 3 from an external IP makes this higher priority than local interactive failures.

## How to Reproduce
1. Download or view `sample-4625-events.log`
2. Open the file in any text editor
3. Count events by source IP and account name
4. Note the Logon Type for each event
5. Document findings using the structure above

## Skills Demonstrated
- Windows Event Log analysis (Event ID 4625)
- Understanding of Logon Types
- Threat identification and prioritization
- MITRE ATT&CK mapping
- Clear SOC-style documentation

## Future Improvements
- Expand the dataset with successful logons (Event ID 4624) for comparison
- Add detection logic or simple scripting
- Build a small lab using Hyper-V or VMware to generate real 4625 events
