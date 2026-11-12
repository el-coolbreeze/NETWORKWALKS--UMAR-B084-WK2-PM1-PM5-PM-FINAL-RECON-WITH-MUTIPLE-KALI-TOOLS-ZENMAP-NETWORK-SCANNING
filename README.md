# NETWORKWALKS--UMAR-B084-WK2-PM1-PM5-PM-FINAL-RECON-WITH-MUTIPLE-KALI-TOOLS-ZENMAP-NETWORK-SCANNING
# Week 2: Cybersecurity & Ethical Hacking Internship Projects

**Organisation:** Networkwalks  
**Project:** Week 2 Practical Tasks  
**Focus Areas:** Footprinting, Reconnaissance, Network Scanning and Penetration Testing Documentation

---

## 📌 Project Overview

This repository contains the practical tasks I completed during Week 2 of my Cybersecurity and Ethical Hacking internship at **Networkwalks**.

The exercises focused on understanding how cybersecurity professionals gather information about a target website, identify publicly exposed infrastructure details, discover active devices on a network, and document their findings in a penetration testing report.

The week consisted of three major activities:

1. **Footprinting and Reconnaissance:** Using six Kali Linux tools to gather information about `networkwalks.com`.
2. **Network Scanning:** Using Zenmap (Nmap GUI) to discover active hosts on my local network.
3. **Penetration Testing Report:** Documenting the methodology, findings, security observations, recommendations and lessons learned.

All activities were conducted for educational purposes within the scope of the assigned practical exercises.

---

## 🎯 Project Objectives

- Understand the importance of reconnaissance in ethical hacking.
- Learn how to gather publicly available information about a domain.
- Identify web technologies, DNS records and HTTP response headers.
- Determine whether a Web Application Firewall (WAF) is protecting a website.
- Understand basic network discovery using Zenmap.
- Identify active devices on a local network.
- Analyse findings and document them in a professional penetration testing report.

---

## 🛠️ Tools and Technologies Used

| Tool | Purpose |
|---|---|
| Kali Linux | Operating system for reconnaissance activities |
| WHOIS | Domain registration information gathering |
| WhatWeb | Website technology fingerprinting |
| Nslookup | DNS lookup and domain-to-IP resolution |
| cURL | HTTP response header inspection |
| Wafw00f | Web Application Firewall detection |
| DNSRecon | DNS record enumeration |
| Zenmap | Graphical network scanning and host discovery |
| Nmap | Network discovery engine used by Zenmap |

---

# PROJECT 1: Footprinting and Reconnaissance Using Kali Linux

**Target Domain:** `networkwalks.com`

Footprinting and reconnaissance are important initial stages of ethical hacking. They involve gathering information about a target to understand its infrastructure, technologies and publicly exposed services.

For this exercise, I used six Kali Linux tools to collect different categories of information about the Networkwalks website.

### 1. WHOIS – Domain Registration Information

**Command used:**

```bash
whois networkwalks.com
```

**Purpose:**

WHOIS retrieves publicly available domain registration information, including the registrar, registration dates, expiry dates and name servers.

**Findings:**

| Information | Result |
|---|---|
| Domain | networkwalks.com |
| Registrar | GoDaddy.com, LLC |
| Creation Date | 6 November 2019 |
| Updated Date | 12 November 2025 |
| Expiry Date | 6 November 2027 |
| Name Server 1 | ns6135.hostgator.com |
| Name Server 2 | ns6136.hostgator.com |
| DNSSEC | Unsigned |
| Domain Status | Client Delete, Renew, Transfer and Update Prohibited |

**Observation:**

The WHOIS lookup revealed that the domain was registered through GoDaddy and uses HostGator name servers. This information provides insight into the domain's registration and DNS infrastructure.

### 2. WhatWeb – Website Technology Fingerprinting

**Command used:**

```bash
whatweb networkwalks.com
```

**Purpose:**

WhatWeb identifies technologies and software components used by a website, including web servers, content management systems, frameworks and plugins.

**Findings:**

| Technology / Information | Result |
|---|---|
| Web Server | Apache |
| Content Management System | WordPress 7.1.4 |
| WordPress Download Manager | 3.3.76 |
| Bootstrap | 7.1.4 |
| jQuery | 3.7.1 |
| Website Title | Networkwalks Academy |
| Server IP | 192.232.216.135 |
| Country | United States |
| Email | info@networkwalks.com |
| HTTP Status | 301 Moved Permanently |
| HTTPS Status | 200 OK |

Additional observations:
- The HTTP version of the website redirects visitors to HTTPS.
- The website uses the `__wpdm_client` cookie.
- The server exposes several HTTP headers, including `permissions-policy`, `referrer-policy` and caching-related headers.

**Observation:**

The scan identified WordPress as the website's CMS and revealed several supporting technologies. This information can help security professionals identify software components that may require security reviews and updates.

### 3. Nslookup – DNS Resolution

**Command used:**

```bash
nslookup networkwalks.com
```

**Purpose:**

Nslookup queries DNS servers to resolve domain names into IP addresses.

**Findings:**

| Information | Result |
|---|---|
| DNS Server | 8.8.8.8 |
| Domain | networkwalks.com |
| Resolved IP Address | 192.232.216.135 |
| Response Type | Non-authoritative answer |

**Observation:**

The domain resolved successfully to the IP address `192.232.216.135`.

This information helps identify the IP address associated with the website and provides a starting point for understanding its network infrastructure.

### 4. cURL – HTTP Response Header Analysis

**Command used:**

```bash
curl -I https://networkwalks.com
```

**Purpose:**

The `-I` option retrieves HTTP response headers without downloading the complete webpage.

**Findings:**

| Header / Information | Result |
|---|---|
| HTTP Protocol | HTTP/2 |
| Status Code | 200 OK |
| Web Server | Apache |
| Content Type | text/html; charset=UTF-8 |
| Referrer Policy | no-referrer-when-downgrade |
| Cache Information | x-nginx-cache: WordPress |
| WordPress API | /wp-json/ |
| Cookie | __wpdm_client |

The response also exposed a WordPress REST API endpoint:

```text
https://networkwalks.com/wp-json/
```

**Observation:**

The HTTP response headers provided additional information about the web server, caching configuration, cookies and WordPress API endpoint.

This exercise demonstrated how HTTP headers can expose technical information about a web application without loading the entire website.

*Note: The actual cookie value has intentionally been excluded from this README.*

### 5. Wafw00f – Web Application Firewall Detection

**Command used:**

```bash
wafw00f networkwalks.com
```

**Purpose:**

Wafw00f identifies whether a website is protected by a Web Application Firewall (WAF).

**Findings:**

```text
[*] Checking https://networkwalks.com

[+] The site https://networkwalks.com
is behind ModSecurity (SpiderLabs) WAF.

[~] Number of requests: 2
```

**Detected WAF:**

ModSecurity (SpiderLabs).

**Observation:**

The scan identified ModSecurity as the Web Application Firewall protecting the website.

A WAF helps monitor and filter potentially malicious web traffic. Its presence is useful defensive information, although detection alone does not establish how effectively it is configured.

### 6. DNSRecon – DNS Enumeration

**Command used:**

```bash
dnsrecon -d networkwalks.com
```

**Purpose:**

DNSRecon enumerates DNS records to gather information about a domain's DNS infrastructure, including name servers, mail servers, TXT records and service records.

**Findings:**

| Record Type | Finding |
|---|---|
| SOA | ns6135.hostgator.com |
| NS | ns6135.hostgator.com |
| NS | ns6136.hostgator.com |
| MX | mail.networkwalks.com |
| A | 192.232.216.135 |
| TXT | Google site verification record |
| TXT | SPF record present |
| SRV | Autodiscover service records |
| DNSSEC | Not configured |
| DNS Software | BIND 9.16.23-RH |
| SRV Records Found | 8 |

**Additional DNS Information:**

The SPF record returned by DNSRecon was:

```text
v=spf1 +a +mx +ip4:50.87.144.87 +include:websitewelcome.com ~all
```

The scan also identified the following name server IP addresses:

```text
ns6135.hostgator.com - 50.87.144.87
ns6136.hostgator.com - 192.232.216.131
```

**Observation:**

DNSRecon revealed information about the domain's name servers, mail infrastructure, SPF configuration and autodiscover service records.

This exercise demonstrated how DNS enumeration can provide a broader picture of an organisation's publicly visible infrastructure.

---

# PROJECT 2: Network Scanning Using Zenmap

### Objective

The objective of this exercise was to perform network discovery on my local network using Zenmap and identify active devices within the subnet.

### Scan Configuration

| Parameter | Value |
|---|---|
| Tool | Zenmap |
| Nmap Version | 7.993 |
| Target Network | 10.17.15.0/24 |
| Scan Type | Ping Scan |
| Total IP Addresses Scanned | 256 |
| Active Hosts Discovered | 2 |
| Scan Duration | 21.52 seconds |

### Nmap Scan Results

The scan returned the following results:

```text
Starting Nmap 7.993 at 2026-11-12 07:09 +0100

Nmap scan report for 10.17.15.142
Host is up (0.0010s latency).
MAC Address: 66:BF:F6:B7:8F:F2 (Unknown)

Nmap scan report for 10.17.15.69
Host is up.

Nmap done: 256 IP addresses (2 hosts up)
scanned in 21.52 seconds.
```

### Discovered Hosts

| Host | IP Address | MAC Address | Status |
|---|---|---|---|
| Host 1 | 10.17.15.142 | 66:BF:F6:B7:8F:F2 | Active |
| Host 2 | 10.17.15.69 | Not reported | Active |

**Total Active Hosts: 2**

One of the two discovered hosts was my personal computer.

### Observation

The Zenmap Ping Scan successfully identified two active hosts on my local subnet, `10.17.15.0/24`.

The exercise demonstrated how Nmap and Zenmap can be used to discover devices that are reachable on a network.

It also highlighted the importance of maintaining an inventory of connected devices so that unexpected or unauthorised devices can be identified.

**Important:** A Ping Scan is a host discovery operation. It does not establish which ports are open or which services are running on the discovered devices.

---

# PROJECT 3: Penetration Testing Report

After completing the reconnaissance and network scanning exercises, I prepared a penetration testing report to document the activities performed and the findings obtained.

The report covers:

- Introduction and objectives.
- Tools and technologies used.
- Reconnaissance methodology.
- WHOIS, WhatWeb, Nslookup, cURL, Wafw00f and DNSRecon findings.
- Zenmap network scanning results.
- Risk analysis and security observations.
- Recommendations.
- Lessons learned and conclusion.
- Screenshots and practical evidence.

The report serves as documentation of the practical exercises completed during Week 2 of my internship.

---

## 🔎 Summary of Findings

| Activity | Key Finding |
|---|---|
| WHOIS | Domain registered through GoDaddy; HostGator name servers identified |
| WhatWeb | Apache, WordPress 7.1.4, WordPress Download Manager 3.3.76 and other technologies identified |
| Nslookup | Domain resolved to 192.232.216.135 |
| cURL | HTTP/2 200 OK; Apache server and WordPress REST API endpoint identified |
| Wafw00f | ModSecurity (SpiderLabs) WAF detected |
| DNSRecon | DNS, mail, SPF, TXT and SRV records identified |
| Zenmap | Two active hosts discovered on 10.17.15.0/24 |
| Documentation | Week 2 penetration testing report prepared |

## ⚠️ Security Observations and Recommendations

The exercises revealed several pieces of information that are useful when evaluating an organisation's security posture.

The following recommendations are based on the observations made during the practical exercises:

1. **Software Updates:** Regularly update WordPress, plugins, frameworks and other website technologies to address known security issues.
2. **Information Disclosure:** Review publicly exposed technology information and minimise unnecessary technical disclosures.
3. **HTTP Security:** Review HTTP response headers and ensure that appropriate security headers and cookie attributes are configured.
4. **DNS Security:** Review DNS records and consider implementing DNSSEC where appropriate.
5. **WAF Protection:** Maintain and properly configure ModSecurity and regularly monitor its security logs.
6. **Network Monitoring:** Perform periodic network discovery to identify devices connected to internal networks.
7. **Device Inventory:** Investigate unfamiliar devices and ensure that only authorised devices have access to the network.

These observations do not constitute confirmed vulnerabilities. Further authorised assessment would be required to validate any potential weaknesses.

---

## 📚 What I Learned

During Week 2 of my internship, I gained practical experience and improved my understanding of the following cybersecurity concepts:

- The importance of footprinting and reconnaissance in ethical hacking.
- How WHOIS can be used to retrieve domain registration information.
- How WhatWeb identifies website technologies and software components.
- How Nslookup resolves domain names into IP addresses.
- How cURL can be used to inspect HTTP response headers.
- How Wafw00f identifies Web Application Firewalls.
- How DNSRecon enumerates DNS records and reveals information about domain infrastructure.
- How Zenmap can be used to discover active devices on a local network.
- The difference between host discovery and port scanning.
- How to document security findings and prepare a penetration testing report.
- The importance of conducting cybersecurity activities within an authorised scope.

The exercises helped me understand how information gathered during reconnaissance can assist security professionals in understanding a target's infrastructure before conducting further security assessments.

---


## 🏁 Conclusion

Week 2 of my Cybersecurity and Ethical Hacking internship at Networkwalks was an opportunity to gain hands-on experience with reconnaissance, footprinting and network discovery tools.

I successfully used six Kali Linux tools to gather information about the `networkwalks.com` domain, including registration details, website technologies, DNS records, HTTP response headers and WAF information.

I also used Zenmap to scan my local network, `10.17.15.0/24`, using the Ping Scan option and successfully identified two active hosts.

Finally, I documented the activities, findings, observations and recommendations in a penetration testing report.

These exercises strengthened my understanding of the importance of information gathering, network discovery, security documentation and responsible ethical hacking practices.

**I look forward to building on these skills as I progress through the remaining weeks of my cybersecurity internship.**

---

## ⚖️ Disclaimer

This repository is intended strictly for educational and cybersecurity learning purposes.

The reconnaissance activities against `networkwalks.com` were performed as part of the assigned Networkwalks internship exercise. Network scanning was restricted to my own local network.

All cybersecurity tools and techniques documented here should only be used on systems and networks for which appropriate authorisation has been obtained.

The author does not support or encourage unauthorised access, malicious activities or misuse of cybersecurity tools.

---

**Internship:** Networkwalks Cybersecurity & Ethical Hacking Programme  
**Week:** 02  
**Project Areas:** Footprinting | Reconnaissance | Network Scanning | Penetration Testing Documentation
