<div align="center">

# 🌐 Networking with CCNA-Level Foundations

### A hands-on DevOps networking module focused on DNS, IP addressing, ports, routing, firewalls and troubleshooting.

![Status](https://img.shields.io/badge/status-in%20progress-yellow)
![Phase](https://img.shields.io/badge/phase-02%20Networking%20Foundations-blue)
![Lessons](https://img.shields.io/badge/lessons-7-lightgrey)
![Level](https://img.shields.io/badge/level-foundation-lightgrey)
![Focus](https://img.shields.io/badge/focus-DevOps%20Networking-orange)

</div>

---

## 📌 Module Overview

This module builds the networking foundation needed for real DevOps work.

Networking connects Linux servers, cloud virtual machines, Docker containers, Kubernetes workloads, databases, monitoring systems and users. This module starts from simple networking concepts and gradually moves toward practical troubleshooting.

The goal is not only to memorize terms, but to understand how network requests move through DNS, IP addresses, gateways, ports, services and firewalls.

---

## 🎯 What This Module Demonstrates

By completing this module, I will practice how to:

- Understand network concepts clearly.
- Work with LAN and WAN basics.
- Understand client/server communication.
- Read IP addresses, routes and gateway information.
- Understand DNS resolution and common DNS records.
- Understand ports and protocols.
- Use Linux troubleshooting commands.
- Inspect listening services and connectivity.
- Understand firewall basics.
- Build a practical networking troubleshooting workflow.

---

## 🧭 Learning Path

| # | Lesson | Focus | Documentation |
|---:|---|---|---|
| 01 | Networking Basics | network concept, LAN, WAN, client/server, IP, gateway, DNS, ports | [notes.md](./lesson-01-networking-basics/notes.md)<br>[notes.hy.md](./lesson-01-networking-basics/notes.hy.md) |
| 02 | IP Addressing | IPv4, private/public IP, subnet mask, CIDR, gateway, loopback | Planned |
| 03 | DNS Basics | domain names, A, CNAME, MX, TXT, `nslookup`, `dig` | Planned |
| 04 | Ports and Protocols | TCP, UDP, HTTP, HTTPS, SSH, DNS, common ports | Planned |
| 05 | Network Troubleshooting | `ping`, `curl`, `wget`, `ss`, `netstat`, `traceroute`, `ip addr`, `ip route` | Planned |
| 06 | Firewalls and Basic Rules | inbound/outbound traffic, `ufw`, allow/deny rules, port security | Planned |
| 07 | Networking Review Lab | DNS troubleshooting, port checks, HTTP/SSH checks, firewall workflow | Planned |

---

## ✅ Completed Lessons

| Lesson | Status | Result |
|---|---|---|
| Lesson 01 — Networking Basics | ✅ Completed | Quiz passed 15/15, documentation ready |

---

## 🛠️ Tools and Commands Practiced

| Category | Commands |
|---|---|
| System info | `hostname`, `whoami`, `date` |
| Network interfaces | `ip addr show` |
| Routing | `ip route` |
| DNS config | `cat /etc/resolv.conf` |
| DNS lookup | `getent hosts` |
| Connectivity | `ping` |
| HTTP/HTTPS checks | `curl -I` |
| Listening ports | `ss -tuln` |
| Output documentation | `tee` |
| Git validation | `git status`, `git add`, `git commit`, `git push` |

---

## 📁 Repository Structure

```text
02-networking-ccna-foundations/
├── README.md
└── lesson-01-networking-basics/
    ├── notes.md
    └── notes.hy.md
```

The lesson lab may also contain output files such as:

```text
system-info.txt
ip-addresses.txt
routing-table.txt
dns-config.txt
dns-lookup.txt
internet-ip-test.txt
dns-ping-test.txt
http-test.txt
listening-ports.txt
network-summary.txt
```

---

## 🌍 Documentation Languages

Each lesson includes two documentation files:

| File | Purpose |
|---|---|
| `notes.md` | Clean English portfolio documentation |
| `notes.hy.md` | Armenian learning and explanation version |

---

## 🚀 Next Step

```text
Lesson 02 — IP Addressing
```

The next lesson will explain IPv4, private/public IP addresses, subnet masks, CIDR, gateway concepts and loopback addresses.
