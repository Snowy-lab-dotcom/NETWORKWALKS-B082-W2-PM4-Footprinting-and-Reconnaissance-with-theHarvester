# 🔎 NETWORKWALKS-B082-W2-PM4-Footprinting-and-Reconnaissance-with-theHarvester

![Cybersecurity](https://img.shields.io/badge/Field-Cybersecurity-red)
![Tool](https://img.shields.io/badge/Tool-theHarvester-blue)
![Platform](https://img.shields.io/badge/Platform-Kali%20Linux-purple)
![Project](https://img.shields.io/badge/Project-Footprinting%20%26%20Reconnaissance-green)
![Purpose](https://img.shields.io/badge/Purpose-Educational-orange)

## 📌 Project Overview

This project demonstrates practical **footprinting and passive reconnaissance** using **theHarvester** in Kali Linux.

The purpose of the exercise was to understand how publicly available information can be collected about an organization from search engines, certificate transparency records, passive DNS sources, and other public information providers.

The practical exercise was completed as part of **Week 2 – Project Module 4 (W2-PM4)** of my cybersecurity training.

### Target Domain

```text
microsoft.com
```

> **Note:** The target domain was provided by the training exercise. The activities documented in this repository were performed for educational cybersecurity training purposes.

---

# 🎯 Objectives

* Use theHarvester in Kali Linux to perform passive reconnaissance on microsoft.com.
* Use Baidu to identify publicly available email addresses and hosts/subdomains.
* Use all available sources in theHarvester to collect additional reconnaissance information.
* Set and use different result limits for each task: 1000 for Baidu and 50 for all sources.
* Review and document the reconnaissance results.

---

# 🛠️ Lab Environment

| Component           | Details                |
| ------------------- | ---------------------- |
| Operating System    | Kali Linux             |
| Tool                | theHarvester           |
| Version             | 4.10.1                 |
| Target              | `microsoft.com`        |
| Reconnaissance Type | Passive Reconnaissance |
| Task 1 Source       | Baidu                  |
| Task 1 Limit        | 1000                   |
| Task 2 Sources      | All available sources  |
| Task 2 Limit        | 50                     |

---

# 🔹 Task 1 – Reconnaissance with Baidu

## Command

```bash
theHarvester -d microsoft.com -l 1000 -b baidu
```

### Command breakdown

| Option | Meaning                     |
| ------ | --------------------------- |
| `-d`   | Specifies the target domain |
| `-l`   | Sets the result limit       |
| `-b`   | Specifies the data source   |

In this task:

```text
-d microsoft.com
-l 1000
-b baidu
```

## 📊 Results

TheHarvester returned the following results from Baidu:

| Category        | Count |
| --------------- | ----: |
| IP addresses    |     0 |
| Email addresses |     1 |
| People          |     0 |
| Hosts           |    12 |

### 📧 Email Address Found

```text
join-ms@microsoft.com
```

### 🌐 Hosts Found

```text
account.microsoft.com
accountprotection.microsoft.com
cla.microsoft.com
cla.opensource.microsoft.com
developer.microsoft.com
docs.microsoft.com
learn.microsoft.com
mtq.microsoft.com
reactor.microsoft.com
schemas.microsoft.com
support.microsoft.com
technet.microsoft.com
```

## 📸 Task 1 Evidence

<img width="602" height="355" alt="image" src="https://github.com/user-attachments/assets/55d7f0cc-4472-4253-ac60-b67fc729feb7" />

---

# 🔹 Task 2 – Reconnaissance Using All Sources

## Command

```bash
theHarvester -d microsoft.com -l 50 -b all
```

This task expanded the reconnaissance by allowing theHarvester to query all available sources supported by the installed configuration.

Some sources require API keys or authentication, so not every source necessarily returned information.

## 📊 Results Summary

The analysis of the scan produced the following results:

| Category                  | Results |
| ------------------------- | ------: |
| Hosts/subdomains          |   9,960 |
| Unique hosts              |   9,527 |
| IP addresses in main list |     147 |
| Inline host-to-IP pairs   |     610 |
| Email addresses           |       3 |
| ASNs                      |       9 |
| Interesting URLs          |       6 |

> **Important:** Hostnames discovered through passive reconnaissance should not automatically be treated as live or publicly reachable systems. Some may originate from DNS records, certificate transparency data, search indexes, cached information, or older infrastructure.

---

# 📧 Email Addresses Identified

The scan returned three email addresses:

```text
dotnet-docker-bot@microsoft.com
opencode@microsoft.com
secure@microsoft.com
```

These were recorded as publicly discovered email addresses. Their current ownership, purpose, or operational status was not independently verified as part of this exercise.

---

# 🌐 Subdomain and Hostname Findings

The scan returned a large number of hostnames.

Some of the larger observed hostname clusters included:

| Domain / Cluster              | Approx. Hosts |
| ----------------------------- | ------------: |
| `corp.microsoft.com`          |         3,459 |
| `cms.microsoft.com`           |           535 |
| `commerce.microsoft.com`      |           438 |
| `communication.microsoft.com` |           217 |
| `cognitive.microsoft.com`     |           131 |
| `fabric.microsoft.com`        |           204 |

These results demonstrate how much information can potentially be collected from public sources during passive reconnaissance.

# 🌍 IP Addresses and ASNs

The scan also returned IP address and ASN information.

The analysis identified:

* **147 IP addresses** in the main results.
* **610 host-to-IP entries** appearing inline with hostname results.
* **9 ASNs**.

The results included infrastructure associated with Microsoft as well as cloud/CDN and other network providers.

<img width="602" height="273" alt="image" src="https://github.com/user-attachments/assets/2ad9381c-69dc-4c8d-9d84-b3ac393c98c2" />

---

# ⚠️ Problems Encountered and Solutions

## 1. Some Sources Required API Keys

When using:

```bash
theHarvester -d microsoft.com -l 50 -b all
```

some sources could not return results because API keys or authentication were required.

### Solution

I reviewed the tool output and continued analysing the sources that were available without additional API credentials.

This helped me understand that theHarvester's results depend on the availability and configuration of individual information sources.

---

## 2. Large Number of Results

The all-source scan produced thousands of hostnames, making the raw output difficult to review manually.

### Solution

I grouped the results using AI into categories such as:

* Emails
* Hosts
* Subdomains
* IP addresses
* ASNs

I also looked for common hostname patterns and domain clusters to make the information easier to interpret.

---

## 3. Results From Different Sources Were Not Consistent

Different sources can provide different information about the same target.

### Solution

I learned that passive reconnaissance results need to be treated as collected intelligence rather than automatically verified facts.

The information should be validated before being used to make conclusions about an organization's infrastructure.

---

## 4. Hostname Does Not Mean Live System

Some discovered hostnames may be old, cached, certificate-related, or otherwise no longer active.

### Solution

I separated **discovery** from **verification**.

TheHarvester was used to identify publicly available information. I did not treat every discovered hostname as a confirmed live system.

---

# 🔐 Security Relevance

Footprinting is an important stage of the reconnaissance process because attackers and security professionals can use publicly available information to build an understanding of an organization's digital footprint.

Information such as:

```text
Email addresses
       ↓
Subdomains
       ↓
Hostnames
       ↓
IP addresses
       ↓
Infrastructure information
```

can provide useful context for understanding an organization's externally visible attack surface.

From a defensive perspective, organizations can perform authorized reconnaissance against their own domains to identify information that may be unnecessarily exposed through public sources.

---

# 🧠 What I Learned

Through this project, I gained practical experience using **theHarvester** for passive reconnaissance.

I learned how to:

* Use theHarvester in Kali Linux.
* Specify a target domain.
* Select individual reconnaissance sources.
* Search using Baidu.
* Use multiple sources with `-b all`.
* Set result limits using the `-l` option.
* Identify publicly available email addresses.
* Identify hosts and subdomains.
* Review IP address and ASN information.
* Analyse large reconnaissance outputs.
* Recognise the limitations of OSINT data.
* Understand why discovered information needs to be validated.
* Document cybersecurity findings clearly and responsibly.

---

# 🧰 Tools & Resources

### Kali Linux: [https://kali.org/get-kali]

### theHarvester

Used to collect publicly available information associated with the target domain.

### Baidu

Used as the search source for Task 1.

---

# ⚖️ Ethical Considerations

This project was completed as part of **authorized cybersecurity education and training**.

The techniques demonstrated should only be used against domains, systems, or organizations where appropriate authorization has been provided.

Passive reconnaissance can reveal information that organizations did not intend to expose publicly. Security professionals should therefore use these techniques responsibly and follow applicable laws, policies, and authorization requirements.

---

# 📌 Disclaimer

**For educational purposes only.**

This repository documents a cybersecurity training exercise. The information-gathering techniques demonstrated here should only be performed within an authorized lab, against systems you own, or against systems where you have explicit permission to conduct security testing.

The results documented in this repository represent information returned by the tools during the exercise and should not be interpreted as a confirmation of vulnerabilities or unauthorized access.

---

# 👤 Author
Malehloa Seroke
Cybersecurity Professional B082

LinkedIn: [www.linkedin.com/in/malehloa-seroke]

---
# 📌 Project Information
Program Name: Cybersecurity at Networkwalks | Week: 02 | Project: WK2-PM1-Footprinting-Reconnaissance-with-Kali-Linux | Repository: GitHub



