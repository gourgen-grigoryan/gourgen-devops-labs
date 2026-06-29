# Lesson 02 — IP Addressing

![Status](https://img.shields.io/badge/status-completed-brightgreen)
![Focus](https://img.shields.io/badge/focus-IP%20addressing-blue)
![Level](https://img.shields.io/badge/level-foundation-lightgrey)

---

## Overview

This lesson covers IPv4 addressing from a DevOps troubleshooting point of view.

IP addressing is one of the most important networking foundations because every server, cloud VM, container, router and service depends on addresses to communicate across a network.

In this lesson, I practiced identifying IPv4 addresses, understanding private and public address ranges, reading CIDR notation, understanding subnet masks at a beginner level, checking the default gateway, validating loopback connectivity and documenting the relationship between `localhost`, `127.0.0.1`, private networks and public access.

---

## Learning Objectives

By completing this lesson, I learned how to:

* understand what an IP address is
* understand the IPv4 address format
* identify valid and invalid IPv4 addresses
* understand private IP ranges
* understand the difference between private and public IP addresses
* understand NAT at a basic level
* understand what a subnet mask does
* understand CIDR notation such as `/24`
* understand what `0.0.0.0/0` means
* identify the default gateway
* understand loopback and `localhost`
* use Linux commands to inspect IP addressing information
* save command outputs for portfolio documentation
* connect IP addressing knowledge to DevOps troubleshooting

---

## Key Concepts

| Concept | Meaning |
| ------- | ------- |
| IP address | A network address used to identify a device |
| IPv4 | IP address format with four octets, such as `192.168.1.25` |
| Octet | One part of an IPv4 address, with a value from `0` to `255` |
| Private IP | IP address used inside private/local networks |
| Public IP | IP address reachable on the Internet |
| NAT | Network Address Translation between private and public addressing |
| Subnet mask | Separates the network part and host part of an IP address |
| CIDR | Short prefix notation such as `/24` |
| `0.0.0.0/0` | All IPv4 addresses / anywhere |
| Gateway | Exit point used to reach other networks |
| Loopback | Local machine network interface |
| `localhost` | Hostname that points to the local machine |

---

## Commands Learned

| Command | Purpose | Example |
| ------- | ------- | ------- |
| `ip -4 addr show` | Show IPv4 addresses | `ip -4 addr show` |
| `hostname -I` | Show IP addresses quickly | `hostname -I` |
| `ip route` | Show routing table and gateway | `ip route` |
| `grep default` | Filter default route | `ip route \| grep default` |
| `awk` | Extract fields from output | `awk '/default/ {print $3; exit}'` |
| `ping` | Test connectivity | `ping -c 4 127.0.0.1` |
| `ip addr show lo` | Show loopback interface | `ip addr show lo` |
| `getent hosts localhost` | Resolve localhost | `getent hosts localhost` |
| `tee` | Save output and show it | `command \| tee file.txt` |

---

## Lab Structure

This lab uses the following folder:

```text
02-networking-ccna-foundations/
└── lesson-02-ip-addressing/
    ├── default-gateway.txt
    ├── gateway-ip.txt
    ├── gateway-ping-test.txt
    ├── hostname-ip.txt
    ├── ip-addressing-summary.txt
    ├── ipv4-addresses.txt
    ├── localhost-lookup.txt
    ├── loopback-interface.txt
    ├── loopback-ping-test.txt
    ├── notes.hy.md
    ├── notes.md
    └── routing-table.txt
```

---

## Practical Commands Used

Create the lesson directory:

```bash
cd ~/devops-labs
mkdir -p 02-networking-ccna-foundations/lesson-02-ip-addressing
cd 02-networking-ccna-foundations/lesson-02-ip-addressing
pwd
```

Show IPv4 addresses:

```bash
ip -4 addr show
```

Save IPv4 address information:

```bash
ip -4 addr show | tee ipv4-addresses.txt
```

Show a quick list of IP addresses:

```bash
hostname -I
```

Save quick IP output:

```bash
hostname -I | tee hostname-ip.txt
```

Show routing table:

```bash
ip route
```

Save routing table:

```bash
ip route | tee routing-table.txt
```

Save the default route:

```bash
ip route | grep default | tee default-gateway.txt
```

Save the gateway IP into a variable:

```bash
GATEWAY_IP=$(ip route | awk '/default/ {print $3; exit}')
echo "Gateway IP: $GATEWAY_IP"
```

Save the gateway IP:

```bash
echo "Gateway IP: $GATEWAY_IP" | tee gateway-ip.txt
```

Ping the gateway:

```bash
ping -c 4 "$GATEWAY_IP"
```

Save gateway ping test:

```bash
ping -c 4 "$GATEWAY_IP" | tee gateway-ping-test.txt
```

Show the loopback interface:

```bash
ip addr show lo
```

Save loopback interface output:

```bash
ip addr show lo | tee loopback-interface.txt
```

Ping the loopback address:

```bash
ping -c 4 127.0.0.1
```

Save loopback ping output:

```bash
ping -c 4 127.0.0.1 | tee loopback-ping-test.txt
```

Resolve `localhost`:

```bash
getent hosts localhost
```

Save localhost lookup:

```bash
getent hosts localhost | tee localhost-lookup.txt
```

Create the IP addressing summary:

```bash
cat > ip-addressing-summary.txt <<'EOF'
# IP Addressing Summary

An IP address identifies a device on a network.

IPv4 addresses have four octets, for example:
192.168.1.25

Each octet can be from 0 to 255.

Private IP ranges:
- 10.0.0.0/8
- 172.16.0.0/12
- 192.168.0.0/16

Public IP addresses are used on the Internet.

A subnet mask separates the network part and host part of an IP address.

CIDR is a shorter way to write subnet information, for example:
192.168.1.25/24

/24 usually means:
- subnet mask 255.255.255.0
- network part: first three octets
- host part: last octet

0.0.0.0/0 means all IPv4 addresses.

A gateway is the exit point used to reach other networks.

Loopback address:
127.0.0.1

localhost points to the local machine.
EOF
```

Validate the folder contents:

```bash
ls -la
```

Check repository status:

```bash
cd ~/devops-labs
git status
```

---

## Understanding IPv4

IPv4 addresses are written as four numbers separated by dots.

Example:

```text
192.168.1.25
```

Each number is called an octet.

```text
192 . 168 . 1 . 25
```

Each octet must be between `0` and `255`.

Valid examples:

```text
192.168.1.10
10.0.0.5
172.16.20.30
8.8.8.8
```

Invalid example:

```text
192.168.1.300
```

This is invalid because `300` is greater than `255`.

---

## Private IP Addresses

Private IP addresses are used inside private networks such as homes, offices, internal cloud networks, Docker networks and lab environments.

Private IP ranges:

```text
10.0.0.0/8
172.16.0.0/12
192.168.0.0/16
```

Common examples:

```text
192.168.1.10
10.0.1.20
172.17.0.2
```

Private IP addresses are not directly reachable from the public Internet without routing, NAT, VPN, load balancers or public mapping.

---

## Public IP Addresses

Public IP addresses are used on the Internet.

A cloud VM may have a public IP address so administrators can connect to it using SSH or expose services through HTTP/HTTPS.

Example model:

```text
Laptop private IP: 192.168.1.25
Router public IP:  89.x.x.x
Cloud VM public IP: 34.x.x.x
```

A DevOps Engineer must understand which IP is internal and which IP is externally reachable.

---

## NAT Basics

NAT means Network Address Translation.

It allows private devices to access the Internet through a public IP address.

Example:

```text
Laptop: 192.168.1.10
Phone:  192.168.1.11
TV:     192.168.1.12
```

These devices may all access the Internet through one router public IP.

```text
Router public IP: 89.x.x.x
```

NAT is important in home networks, cloud networking, Docker networking and Kubernetes networking.

---

## Subnet Mask

A subnet mask separates the network part and host part of an IP address.

Example:

```text
IP:          192.168.1.25
Subnet mask: 255.255.255.0
```

In beginner-friendly terms:

```text
Network part: 192.168.1
Host part:    25
```

Devices in the same `/24` network often share the first three octets.

Example same network:

```text
192.168.1.10
192.168.1.25
192.168.1.100
```

Example different network:

```text
192.168.2.25
```

---

## CIDR Notation

CIDR is a shorter way to write network prefix information.

Example:

```text
192.168.1.25/24
```

The `/24` means the first 24 bits are the network prefix.

Beginner-friendly meaning:

```text
Network: 192.168.1.0
Hosts:   192.168.1.x
```

Common examples:

| CIDR | Subnet mask | Meaning |
| ---- | ----------- | ------- |
| `/8` | `255.0.0.0` | Large network |
| `/16` | `255.255.0.0` | Large private/cloud network |
| `/24` | `255.255.255.0` | Common small LAN subnet |
| `/32` | `255.255.255.255` | One specific IP address |

---

## Understanding `0.0.0.0/0`

`0.0.0.0/0` means all IPv4 addresses.

In firewall or cloud security rules, it means anywhere on the Internet.

Example:

```text
SSH port 22 open to 0.0.0.0/0
```

This means SSH is open to the entire Internet.

For production systems, this is often unsafe. SSH access should normally be restricted to trusted IP addresses, VPN, bastion hosts or other controlled access patterns.

---

## Gateway

A gateway is the exit point used to reach other networks.

Example:

```text
Your IP: 192.168.1.25
Gateway: 192.168.1.1
```

If the destination is outside the local network, the system sends traffic to the gateway.

```text
Laptop → Gateway/Router → Internet → Server
```

Linux command:

```bash
ip route
```

Typical output:

```text
default via 192.168.1.1 dev eth0
```

`default via` indicates the default gateway.

---

## Loopback and Localhost

The loopback address points to the local machine.

```text
127.0.0.1
```

`localhost` usually resolves to the local machine.

```text
localhost → 127.0.0.1
```

When an application is running locally, it may be accessed as:

```text
http://localhost:3000
http://127.0.0.1:3000
```

This is used frequently in local development, Docker, Nginx reverse proxy testing, systemd service validation and Kubernetes port-forwarding.

---

## DevOps Troubleshooting Examples

### IP exists but gateway is missing

If `ip -4 addr show` shows an IP address but `ip route` does not show a `default via` route, the system may be connected locally but unable to reach outside networks.

### Private IP does not mean public access

A server with only a private IP such as `10.0.1.10` is usually not directly accessible from the Internet.

It may require:

* public IP
* NAT
* VPN
* load balancer
* bastion host
* routing rule
* firewall rule

### SSH open to the world

If SSH is open to `0.0.0.0/0`, it is reachable from anywhere on the Internet.

This is risky for production environments and should be restricted.

---

## Quick Reference

| Task | Command |
| ---- | ------- |
| Show IPv4 addresses | `ip -4 addr show` |
| Show quick IP list | `hostname -I` |
| Show routes | `ip route` |
| Show default gateway | `ip route \| grep default` |
| Save gateway variable | `GATEWAY_IP=$(ip route \| awk '/default/ {print $3; exit}')` |
| Ping gateway | `ping -c 4 "$GATEWAY_IP"` |
| Show loopback interface | `ip addr show lo` |
| Ping loopback | `ping -c 4 127.0.0.1` |
| Resolve localhost | `getent hosts localhost` |

---

## Common Mistakes

| Mistake | Problem | Correct Practice |
| ------- | ------- | ---------------- |
| Thinking every IP is public | Private IPs are not directly Internet reachable | Identify private vs public IPs |
| Confusing `/24` with a port | `/24` is a network prefix length | Ports are separate from CIDR |
| Opening SSH to `0.0.0.0/0` | Exposes SSH to the whole Internet | Restrict SSH to trusted IPs |
| Ignoring the gateway | No default gateway can break Internet access | Check `ip route` |
| Confusing `localhost` with a remote server | `localhost` points to the local machine | Use the correct remote IP or domain |

---

## Validation Checklist

| Check | Status |
| ----- | ------ |
| Lesson directory created | ✅ Completed |
| IPv4 addresses inspected | ✅ Completed |
| Gateway checked | ✅ Completed |
| Gateway IP saved | ✅ Completed |
| Loopback interface checked | ✅ Completed |
| Localhost resolution checked | ✅ Completed |
| Summary file created | ✅ Completed |
| Quiz completed | ✅ Passed |

---

## Quiz Result

```text
Score: 15/15 after correction
Status: Passed
```

The missed answer was corrected:

```text
192.168.1.25/24
```

`/24` means network prefix length, not SSH port.

---

## Git Workflow

After placing this lesson documentation in the repository, use specific paths:

```bash
cd ~/devops-labs

git status

git add README.md ROADMAP.md 02-networking-ccna-foundations/README.md 02-networking-ccna-foundations/lesson-02-ip-addressing

git commit -m "Complete IP addressing lesson"

git push

git status
```

Expected final result:

```text
nothing to commit, working tree clean
```

---

## What I Learned

In this lesson, I learned how IPv4 addressing works at a practical DevOps level. I learned how to identify private and public IP addresses, understand CIDR notation, read default gateway information, validate loopback connectivity and connect these concepts to real troubleshooting situations.

---

## Final Status

Lesson completed, quiz passed, committed and pushed to GitHub.
