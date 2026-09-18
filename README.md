# 🔐 NETWORK-WALKS-B083-WK2-PM-FINAL--FOOTPRINTING-AND-RECONNAISSANCE-PHASE

**FOOTPRINTING & RECONNAISANCE PHASES**
</div>

<p align="center">
  <img src="https://img.shields.io/badge/Skill-Cybersecurity-404040?style=flat-square&labelColor=C00000" />
  <img src="https://img.shields.io/badge/Kali%20Linux-v2026.2-E87500?style=flat-square&labelColor=000000&logo=kalilinux&logoColor=white" />
  <img src="https://img.shields.io/badge/Skill-Linux%20tools-404040?style=flat-square&labelColor=C00000" />
  <img src="https://img.shields.io/badge/Network-10.0.0.0%2F24-238F89?style=flat-square&labelColor=000000" />
  <img src="https://img.shields.io/badge/Penetration%20Testing-C00000?style=flat-square&labelColor=000000&logo=kalilinux&logoColor=white" />
  <img src="https://img.shields.io/badge/Skill-Footprinting-404040?style=flat-square&labelColor=C00000" />
  <img src="https://img.shields.io/badge/GitHub-404040?style=flat-square&labelColor=0070C0&logo=github&logoColor=white" />
  <img src="https://img.shields.io/badge/Whois%20nslookup%20whatweb%20curl -%20wafwoof%20dnsrecon-404040?style=flat-square&labelColor=C00000&logo=kalilinux&logoColor=white" />
  <img src="https://img.shields.io/badge/NetworkWalks-404040?style=flat-square&labelColor=C00000" />
  <img src="https://img.shields.io/badge/Reconaissance%20&%20Footprinting%20with%20Maltego-E87500?style=flat-square&labelColor=000000&logo=kalilinux&logoColor=white" />
  <img src="https://img.shields.io/badge/Idongesit%20Nkanga%Internship-C00000?style=flat-square" />
</p>

---
| Field | Details |
|---|---|
| Pentester Name | **IDONGESIT NKANGA** |
| Program/Batch | B083-Networkwalks |
| Date | 17 September 2026 |
| Modules completed | W2-PM1 (Multiple Kali Tools)<br>W2-PM5 (Zenmap Scanning) |
| Client/Target | Networkwalks (secured written permission already) |
| Permission secured from client? | Yes |
| Phases covered | Phase 1: Reconnaissance & Footprinting<br>Phase 2: Scanning & Network Discovery<br>Phase 3-5: In Progress |

---

## 1. Liability Disclaimer

I have performed these activities only on the systems & devices where I had secured written permission or the devices/systems that I own myself. All these materials are for education and research purpose only. The instructor, the authors and Networkwalks are not responsible for what I do with this knowledge. I understand that every action I take is my own responsibility and misuse can lead to criminal charges, heavy fines, loss of job and a permanent record.

## 2. Introduction

This report covers footprinting the networkwalks.com domain using multiple Kali Linux tools (W2-PM1) and Maltego (W2-PM3). The modules covered shows how an attacker can gather these public information and use it to launch vulnerability-related attacks. It is the Week 2 part of my ongoing internship program at Networkwalks.

All commands were run in Kali Linux (footprinting) and on Maltego App installed. Every step below includes the exact command used, the result I observed, a screenshot as evidence, and a short note on why the finding matters from an attacker's point of view.

## 3. Tools Used

| Tool | Purpose |
|---|---|
| Kali Linux & Windows | Operating systems used for reconnaissance activities |
| WHOIS | Find domain registration details (owner, dates, name servers). |
| whatweb | Fingerprint web technologies (server, CMS, plugins, IP). |
| nslookup | Resolve the domain name to its IP address using DNS. |
| curl -I | Read the HTTP response headers of the website. |
| wafw00f | Detect whether a Web Application Firewall protects the site. |
| dnsrecon | Enumerate all DNS records (NS, MX, SPF, TXT, SRV). |
| Maltego Graph | Find all email addresses related to the target organization domain |

## 4. Activities Performed

### 4.1 Footprinting & Reconnaissance with Kali Linux tools

I performed reconnaissance against the networkwalks.com domain using six Kali Linux tools: WHOIS, WhatWeb, Nslookup, Curl, Wafw00f and DNSRecon. Each tool was used to collect a different type of information about the target.

First, I used WHOIS to obtain publicly available domain registration information and identify the domain’s name servers. The results provided information about the domain registration and hosting infrastructure.

I then used WhatWeb to identify technologies used by the website. The results identified WordPress 7.0.4 and WP Download Manager 3.3.58, along with other information exposed by the website.

Using Nslookup, I resolved the domain name to its IP address. The provided result identified **192.232.216.135**.

I used Curl with the `-I` option to inspect the HTTP response headers. This provided additional information about the web application and exposed the WordPress REST API endpoint `/wp-json/`.

Next, I used Wafw00f to determine whether a Web Application Firewall was protecting the website. The result identified **ModSecurity (SpiderLabs)**.

Finally, I used DNSRecon to enumerate DNS records. The results provided information relating to name servers, mail servers, SPF/TXT records, service records and DNS software information.

### 4.2 Footprinting with Maltego

For the second activity, I used maltego to perform a passive recognaissance and information gathering against networkwalks.com to identify exposed organizational details.

**Primary Findings:** I successfully harvested public organizational email asset (networkwalks.com) using automated Maltego transforms.

**Methodology:** The first task was to install, set up and activate Maltego. I downloaded and installed Maltego v4.12.1 along with required JAVA JRE dependencies, configured and authenticated the software via Maltego ID. When the activation and set up was completed, I then launched the app, created a new investigation graph and mapped the primary Domain entity (networkwalks.com).

I executed email discovery transforms and got the findings below:

| Entity Type | Discovered Value | Discovery Source / Transform |
|---|---|---|
| Domain | Networkwalks.com | Target Domain Entry |
| Email Address (s) | info@networkwalkss.com<br>abuse@godaddy.com | Search Engine & Whois Transform |

## 5. Risk Analysis / Impact

Based on the information collected during the footprinting and network scanning activities, I identified the following potential risks.

| # | Risk / Finding | Evidence / Observation | Potential Impact | Risk Level |
|---:|---|---|---|---|
| 1 | Web technology information exposed | WhatWeb identified WordPress and WP Download Manager | Attackers may use exposed technology/version information to identify software requiring further security review | **Medium** |
| 2 | Server IP address identifiable | Nslookup resolved the domain to 192.232.216.135 | Provides information about the network location of the web service | **Low** |
| 3 | HTTP technical information exposed | Curl returned HTTP response headers and exposed /wp-json/ | May assist technology fingerprinting and further enumeration | **Low** |
| 4 | WAF technology identifiable | Wafw00f identified ModSecurity (SpiderLabs) | Reveals information about the web application’s security architecture | **Low** |
| 5 | DNS infrastructure information exposed | DNSRecon identified DNS, mail and service-related records | DNS information can help build a broader infrastructure profile | **Medium** |
| 6 | Email addresses related to the target organization domain | Maltego harvested two public organization emai assets | Information gathering exposure which may serve as entry points for phishing and pretexting campaigns. | **Low** |

**Risk level key:** Critical · Medium · Low

> The risks above are observations from the footprinting exercise, not confirmed vulnerabilities.
>
> The practical exercises primarily involved information gathering. No exploitation or vulnerability validation was performed as part of these two modules.
>
> Therefore, the presence of information such as a software version, IP address or DNS record does not by itself mean that the system is vulnerable. Further authorized security testing would be required to confirm any actual vulnerability.

## 6. Recommendations

Based on the observations from these activities, I recommend the following security improvements:

1. **Review publicly exposed technology information**  
   Organizations should regularly review what information about their web technologies, CMS and plugins is publicly visible.

2. **Keep software updated**  
   CMS platforms, plugins and other web technologies should be regularly updated and reviewed against current security advisories.

3. **Review HTTP headers**  
   HTTP response headers should be reviewed to determine whether unnecessary technical information is being exposed.

4. **Review DNS records regularly**  
   DNS records should be checked periodically to ensure that only required information and services are publicly exposed.

5. **Properly configure and monitor the WAF**  
   Keep the WAF (ModSecurity) enabled and tuned, since it already blocks naive attacks.

6. **Perform regular internal network discovery**  
   Organizations should periodically scan their own networks to identify active devices.

7. **Investigate unknown devices**  
   Any unexpected device discovered during network scanning should be investigated and verified.

8. **Maintain network documentation**  
   Network topology and device information should be documented and updated regularly.

9. **Whois Privacy**  
   Implement privacy protection servuces to mask administrative and technical contact details in WHOIS records.

10. **Email Security**  
    Enforce Multi-Factor Authentication (MFA) and strict SPF/DKIM/DMARC records for all corporate communication channels.

## 7. Conclusion

During Week 2 of my Cybersecurity & Ethical Hacking internship, I completed practical activities covering footprinting and passive reconnaissance.

In the footprinting activity with Kali Linux, I used six tools to collect information about the target domain. I learned how WHOIS can provide domain information, WhatWeb can identify web technologies, Nslookup can resolve domain names, Curl can inspect HTTP headers, Wafw00f can identify a WAF, and DNSRecon can provide additional DNS information.

In the footprinting with Maltego, I launch a new investigation graph to mapped the primary Domain entity, and then used the email transform tool to harvest the organization’s email assets.

The exercises showed me that information gathering is an important part of cybersecurity. Even before attempting to exploit a system, a security professional can learn a significant amount about an environment by carefully analyzing publicly available information and network responses.

I also learned that technical findings should be documented clearly. A good cybersecurity report should explain what was performed, what was discovered, what the observation means, what risk it may create, and what can be done to reduce that risk.

Finally, I learned that reconnaissance and scanning must always be performed within an authorized scope. These activities were completed as part of the assigned educational cybersecurity lab.

## 8. Evidences Collected

The original report contains evidence screenshots collected during the practical activities.

![Evidence 1](evidence/repo_evidence_1.png)

![Evidence 2](evidence/repo_evidence_2.png)

![Evidence 3](evidence/repo_evidence_3.png)

![Evidence 4](evidence/repo_evidence_4.png)

![Evidence 5](evidence/repo_evidence_5.png)

![Evidence 6](evidence/repo_evidence_6.png)

![Evidence 7](evidence/repo_evidence_7.png)

![Evidence 8](evidence/repo_evidence_8.png)

---

## Author

**IDONGESIT NKANGA**  
Cybersecurity Intern — B083

LinkedIn: https://www.linkedin.com/in/ idongesit-george-7b0125a8

### Project Information

- **Program Name:** Cybersecurity program at Networkwalks
- **Week:** 02
- **Repository:** GitHub

