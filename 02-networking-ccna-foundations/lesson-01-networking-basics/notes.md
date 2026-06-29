# Lesson 01 — Networking Basics

![Status](https://img.shields.io/badge/status-completed-brightgreen)
![Focus](https://img.shields.io/badge/focus-networking%20basics-blue)
![Level](https://img.shields.io/badge/level-foundation-lightgrey)

---

## Overview

This lesson introduces the basic networking concepts required for DevOps work.

Networking is the foundation behind servers, cloud infrastructure, Docker, Kubernetes, DNS, firewalls, SSH, monitoring and production troubleshooting. A DevOps Engineer must understand how devices communicate, how requests reach servers, how DNS translates names, how gateways move traffic outside the local network and how ports identify services.

In this lesson, I learned the meaning of a network, LAN, WAN, client/server communication, IP addresses, gateways, DNS and ports. I also practiced basic Linux networking inspection commands and saved outputs as portfolio evidence.

---

## Learning Objectives

By completing this lesson, I learned how to:

* understand what a network is
* explain the difference between LAN and WAN
* understand the client/server model
* understand the purpose of IP addresses
* understand the role of a gateway
* understand how DNS translates domain names into IP addresses
* understand what ports are used for
* recognize common ports such as SSH, DNS, HTTP and HTTPS
* inspect IP addresses using `ip addr show`
* inspect routes and the default gateway using `ip route`
* inspect DNS configuration using `/etc/resolv.conf`
* test DNS resolution using `getent hosts`
* test IP connectivity using `ping`
* test HTTPS responses using `curl -I`
* inspect listening ports using `ss -tuln`
* document a basic networking troubleshooting workflow

---

## Key Concepts

| Concept | Meaning |
| ------- | ------- |
| Network | A connection between devices so they can exchange data |
| Host | Any device connected to a network and identified by an IP address |
| Client | A device or program that sends a request |
| Server | A device or program that receives requests and returns responses |
| LAN | Local Area Network, such as a home or office network |
| WAN | Wide Area Network, a larger network connecting multiple networks |
| Internet | The largest public WAN |
| IP address | A network address used to identify a device |
| Private IP | An IP address used inside a local network |
| Public IP | An IP address reachable on the Internet |
| Gateway | The exit point used to reach networks outside the local network |
| DNS | System that translates domain names into IP addresses |
| Port | A service-specific communication endpoint on a server |

---

## Commands Learned

| Command | Purpose | Example |
| ------- | ------- | ------- |
| `hostname` | Shows the system hostname | `hostname` |
| `whoami` | Shows the current user | `whoami` |
| `date` | Shows the current date and time | `date` |
| `command -v COMMAND` | Checks whether a command exists | `command -v curl` |
| `ip addr show` | Shows network interfaces and IP addresses | `ip addr show` |
| `ip route` | Shows routing table and default gateway | `ip route` |
| `cat /etc/resolv.conf` | Shows DNS resolver configuration | `cat /etc/resolv.conf` |
| `getent hosts DOMAIN` | Resolves a domain name to IP addresses | `getent hosts github.com` |
| `ping -c 4 IP` | Tests IP connectivity | `ping -c 4 8.8.8.8` |
| `ping -c 4 DOMAIN` | Tests DNS plus network connectivity | `ping -c 4 github.com` |
| `curl -I URL` | Requests HTTP/HTTPS response headers | `curl -I https://github.com` |
| `ss -tuln` | Shows listening TCP/UDP ports | `ss -tuln` |
| `tee FILE` | Prints output and writes it to a file | `ip route \| tee routing-table.txt` |

---

## Lab Structure

In this lab, the following lesson structure is used:

```text
lesson-01-networking-basics/
|-- dns-config.txt
|-- dns-lookup.txt
|-- dns-ping-test.txt
|-- http-test.txt
|-- internet-ip-test.txt
|-- ip-addresses.txt
|-- listening-ports.txt
|-- network-summary.txt
|-- notes.hy.md
|-- notes.md
|-- routing-table.txt
`-- system-info.txt
```

---

## Practical Commands Used

Create the lesson directory:

```bash
cd ~/devops-labs
mkdir -p 02-networking-ccna-foundations/lesson-01-networking-basics
cd 02-networking-ccna-foundations/lesson-01-networking-basics
pwd
```

Check required tools:

```bash
command -v ip
command -v ping
command -v curl
command -v ss
```

Install basic tools if needed:

```bash
sudo apt update
sudo apt install -y iproute2 iputils-ping curl
```

Save system information:

```bash
{
  echo "Hostname:"
  hostname

  echo
  echo "Current user:"
  whoami

  echo
  echo "Current date:"
  date
} | tee system-info.txt
```

Inspect IP addresses:

```bash
ip addr show
ip addr show | tee ip-addresses.txt
```

Inspect routes and default gateway:

```bash
ip route
ip route | tee routing-table.txt
```

Inspect DNS configuration:

```bash
cat /etc/resolv.conf
cat /etc/resolv.conf | tee dns-config.txt
```

Resolve a domain name:

```bash
getent hosts github.com
getent hosts github.com | tee dns-lookup.txt
```

Test Internet connectivity by IP:

```bash
ping -c 4 8.8.8.8
ping -c 4 8.8.8.8 | tee internet-ip-test.txt
```

Test DNS and network connectivity together:

```bash
ping -c 4 github.com
ping -c 4 github.com | tee dns-ping-test.txt
```

Test HTTPS response headers:

```bash
curl -I https://github.com
curl -I https://github.com | tee http-test.txt
```

Inspect local listening ports:

```bash
ss -tuln
ss -tuln | tee listening-ports.txt
```

Create a summary file:

```bash
cat > network-summary.txt <<'EOF'
# Networking Basics Summary

A network connects devices so they can exchange data.

LAN means Local Area Network. It is used inside a home, office or local environment.

WAN means Wide Area Network. The Internet is the largest public WAN.

A client sends requests. A server receives requests and returns responses.

An IP address identifies a device on a network.

A gateway is the exit point used to reach networks outside the local network.

DNS translates domain names into IP addresses.

Ports identify specific services running on a server.

Common ports:
- 22 SSH
- 53 DNS
- 80 HTTP
- 443 HTTPS

Basic troubleshooting idea:
- If IP ping works but domain ping fails, suspect DNS.
- If DNS works but HTTP fails, suspect service, port, firewall, TLS or application issue.
- If no network works, check IP address, route, gateway and connectivity.
EOF
```

Check files:

```bash
ls -la
```

---

## Understanding Networking

A network connects devices so they can exchange data.

Examples of networked devices include laptops, phones, routers, printers, servers, cloud virtual machines and containers.

In DevOps, networking is required for almost everything:

* SSH access to servers
* web traffic to applications
* DNS records for domains
* Nginx reverse proxies
* database connections
* Docker container communication
* Kubernetes service discovery
* firewall rules
* monitoring endpoints
* cloud networking

A simple request often depends on several network layers working correctly.

---

## LAN and WAN

A LAN is a Local Area Network. It is usually used inside a home, office or local environment.

Example LAN:

```text
Laptop -> Router -> Phone -> Printer
```

A WAN is a Wide Area Network. It connects larger networks together. The Internet is the largest public WAN.

Example path:

```text
Laptop -> Home router -> ISP network -> Internet -> Cloud server
```

---

## Client and Server

The client/server model is one of the most important networking models.

A client sends a request. A server receives the request and returns a response.

Example:

```text
Browser  -> request  -> Web server
Browser  <- response <- Web server
```

When opening `https://github.com`, the browser is the client and GitHub's web infrastructure is the server side.

---

## IP Addresses

An IP address identifies a device on a network.

Examples:

```text
192.168.1.25
10.0.0.5
8.8.8.8
```

Private IP addresses are used inside local networks. Public IP addresses are used on the Internet.

Common private IP ranges include:

```text
10.0.0.0/8
172.16.0.0/12
192.168.0.0/16
```

---

## Gateway

A gateway is the exit point used to reach networks outside the local network.

If a destination is not inside the local network, the system sends traffic through the default gateway.

Linux command:

```bash
ip route
```

Typical default gateway line:

```text
default via 192.168.1.1 dev eth0
```

---

## DNS

DNS translates domain names into IP addresses.

Humans use names such as:

```text
github.com
example.com
fashionstation.am
```

Computers communicate using IP addresses. DNS performs the translation.

Example:

```text
github.com -> IP address
```

Linux DNS resolver configuration can be inspected with:

```bash
cat /etc/resolv.conf
```

A domain can be resolved with:

```bash
getent hosts github.com
```

---

## Ports

A port identifies a specific service on a server.

One server can run many services on the same IP address, but each service listens on a different port.

Common ports:

| Service | Port |
| ------- | ---: |
| SSH | 22 |
| DNS | 53 |
| HTTP | 80 |
| HTTPS | 443 |
| PostgreSQL | 5432 |
| MySQL | 3306 |
| Node.js development app | 3000 |

If a service is not listening on the expected port, clients cannot connect to it even if the server is reachable.

---

## Basic Troubleshooting Logic

A simple DevOps troubleshooting chain:

```text
Domain -> DNS -> IP -> Gateway -> Server -> Port -> Response
```

Useful checks:

| Problem | Possible Area |
| ------- | ------------- |
| IP ping works, domain ping fails | DNS issue |
| DNS works, HTTPS fails | service, port, firewall, TLS or application issue |
| No default route exists | gateway or routing issue |
| Expected port is not visible in `ss -tuln` | service may not be running or listening |

---

## Validation

Run these commands from the lesson directory:

```bash
pwd
ls -la
cat system-info.txt
cat ip-addresses.txt
cat routing-table.txt
cat dns-config.txt
cat dns-lookup.txt
cat internet-ip-test.txt
cat dns-ping-test.txt
cat http-test.txt
cat listening-ports.txt
cat network-summary.txt
```

Expected result:

* lesson directory exists
* `notes.md` exists
* `notes.hy.md` exists
* networking output files exist
* IP addresses were inspected
* routing table and default gateway were checked
* DNS resolver configuration was checked
* DNS resolution was tested
* IP connectivity was tested
* HTTPS response headers were tested
* local listening ports were inspected
* a networking summary was documented

---

## Quiz Review

| # | Question | Correct Answer | Status |
|---:|---|---|---|
| 1 | What is a network? | A connection between devices so they can send and receive data. | Passed |
| 2 | What is a LAN? | A Local Area Network used in a home, office or local environment. | Passed |
| 3 | What is a WAN? | A Wide Area Network that connects larger networks. | Passed |
| 4 | What role does the browser have when opening `https://github.com`? | Client. | Passed |
| 5 | What does a server do? | Receives requests and returns responses. | Passed |
| 6 | What is an IP address used for? | It identifies a device on a network. | Passed |
| 7 | What is the role of a gateway? | It is the exit point from the local network to outside networks. | Passed |
| 8 | What does DNS do? | It translates domain names into IP addresses. | Passed |
| 9 | What does a port represent? | A service-specific door or endpoint on a server. | Passed |
| 10 | Which port is usually used for HTTPS? | 443. | Passed |
| 11 | Which port is usually used for SSH? | 22. | Passed |
| 12 | If IP ping works but domain ping fails, what is likely wrong? | DNS. | Passed |
| 13 | Which command shows the default gateway? | `ip route`. | Passed |
| 14 | Which command shows local listening ports? | `ss -tuln`. | Passed |
| 15 | What does `curl -I https://github.com` check? | HTTPS response headers. | Passed |

### Quiz Result

```text
Lesson quiz: Passed — 15/15
```

Lesson quiz passed successfully.

---

## Troubleshooting Notes

If IP connectivity works but domain connectivity fails, check DNS:

```bash
ping -c 4 8.8.8.8
ping -c 4 github.com
cat /etc/resolv.conf
getent hosts github.com
```

If DNS works but HTTPS fails, check service, port, firewall or TLS/application behavior:

```bash
getent hosts github.com
curl -I https://github.com
```

If the system has no default gateway, inspect routes:

```bash
ip route
```

If a local application should listen on a port, verify with:

```bash
ss -tuln
```

---

## Git Workflow

After completing the lesson and passing the quiz, the work will be saved using Git:

```bash
cd ~/devops-labs
git status
git add README.md ROADMAP.md 02-networking-ccna-foundations
git commit -m "Complete networking basics lesson"
git push
git status
```

Expected final result:

```text
nothing to commit, working tree clean
```

---

## What I Learned

In this lesson, I learned the basic networking concepts required for DevOps.

I learned how LAN, WAN, clients, servers, IP addresses, gateways, DNS and ports work together when a request travels from a computer to a server.

I also practiced Linux networking inspection commands and learned a basic troubleshooting flow for DNS, connectivity, routes, gateways, ports and services.

---

## Status

Lesson completed, quiz passed, ready to commit and push.
