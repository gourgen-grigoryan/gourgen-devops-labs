# Lesson 01 — Networking Basics

![Status](https://img.shields.io/badge/status-completed-brightgreen)
![Focus](https://img.shields.io/badge/focus-networking%20basics-blue)
![Level](https://img.shields.io/badge/level-foundation-lightgrey)

---

## Overview

Այս դասը բացատրում է DevOps-ի համար անհրաժեշտ networking-ի հիմնական գաղափարները։

Networking-ը հիմք է servers-ի, cloud infrastructure-ի, Docker-ի, Kubernetes-ի, DNS-ի, firewalls-ի, SSH-ի, monitoring-ի և production troubleshooting-ի համար։ DevOps Engineer-ը պետք է հասկանա՝ ինչպես են devices-ը կապվում իրար հետ, ինչպես request-ը հասնում է server-ին, ինչպես DNS-ը name-ը փոխում է IP-ի, ինչպես gateway-ը դուրս է ուղարկում traffic-ը local network-ից և ինչպես ports-ը ցույց են տալիս services-ը։

Այս դասում ես սովորեցի network, LAN, WAN, client/server communication, IP address, gateway, DNS և ports հասկացությունները։ Նաև գործնականում օգտագործեցի Linux networking inspection commands և output-ները պահեցի որպես portfolio evidence։

---

## Learning Objectives

Այս դասից հետո ես սովորեցի՝

* ինչ է network-ը
* ինչ տարբերություն կա LAN-ի և WAN-ի միջև
* ինչ է client/server model-ը
* ինչի համար է IP address-ը
* ինչ դեր ունի gateway-ը
* ինչպես DNS-ը domain name-ը փոխում է IP address-ի
* ինչ է port-ը server-ի վրա
* ճանաչել common ports՝ SSH, DNS, HTTP և HTTPS
* ստուգել IP addresses-ը `ip addr show` command-ով
* ստուգել routes-ը և default gateway-ը `ip route` command-ով
* ստուգել DNS configuration-ը `/etc/resolv.conf` file-ով
* ստուգել DNS resolution-ը `getent hosts` command-ով
* ստուգել IP connectivity-ն `ping` command-ով
* ստուգել HTTPS response-ը `curl -I` command-ով
* ստուգել listening ports-ը `ss -tuln` command-ով
* գրել basic networking troubleshooting workflow

---

## Key Concepts

| Concept | Բացատրություն |
| ------- | ------------- |
| Network | Devices-ի կապ, որպեսզի նրանք կարողանան data փոխանակել |
| Host | Ցանկացած device, որը network-ում ունի IP address |
| Client | Device կամ program, որը request է ուղարկում |
| Server | Device կամ program, որը request է ստանում և response վերադարձնում |
| LAN | Local Area Network՝ տուն, office կամ local environment |
| WAN | Wide Area Network՝ մեծ network, որը միացնում է տարբեր network-ներ |
| Internet | Ամենամեծ public WAN-ը |
| IP address | Network address, որով device-ը ճանաչվում է network-ում |
| Private IP | IP address, որը օգտագործվում է local network-ի ներսում |
| Public IP | IP address, որը հասանելի է Internet-ում |
| Gateway | Local network-ից դուրս գնալու ելքի կետ |
| DNS | System, որը domain name-ը փոխում է IP address-ի |
| Port | Server-ի վրա կոնկրետ service-ի communication endpoint |

---

## Commands Learned

| Command | Նպատակ | Օրինակ |
| ------- | ------ | ------ |
| `hostname` | Ցույց է տալիս system hostname-ը | `hostname` |
| `whoami` | Ցույց է տալիս current user-ը | `whoami` |
| `date` | Ցույց է տալիս current date/time-ը | `date` |
| `command -v COMMAND` | Ստուգում է command-ը կա, թե ոչ | `command -v curl` |
| `ip addr show` | Ցույց է տալիս network interfaces և IP addresses | `ip addr show` |
| `ip route` | Ցույց է տալիս routing table և default gateway | `ip route` |
| `cat /etc/resolv.conf` | Ցույց է տալիս DNS resolver configuration-ը | `cat /etc/resolv.conf` |
| `getent hosts DOMAIN` | Domain name-ը resolve է անում IP address-ի | `getent hosts github.com` |
| `ping -c 4 IP` | Ստուգում է IP connectivity | `ping -c 4 8.8.8.8` |
| `ping -c 4 DOMAIN` | Ստուգում է DNS + network connectivity | `ping -c 4 github.com` |
| `curl -I URL` | Ստանում է HTTP/HTTPS response headers | `curl -I https://github.com` |
| `ss -tuln` | Ցույց է տալիս listening TCP/UDP ports | `ss -tuln` |
| `tee FILE` | Output-ը ցույց է տալիս և գրում file-ի մեջ | `ip route \| tee routing-table.txt` |

---

## Lab Structure

Այս lab-ում օգտագործվում է հետևյալ lesson structure-ը՝

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

Ստեղծել lesson directory՝

```bash
cd ~/devops-labs
mkdir -p 02-networking-ccna-foundations/lesson-01-networking-basics
cd 02-networking-ccna-foundations/lesson-01-networking-basics
pwd
```

Ստուգել required tools-ը՝

```bash
command -v ip
command -v ping
command -v curl
command -v ss
```

Եթե պետք է, տեղադրել basic tools՝

```bash
sudo apt update
sudo apt install -y iproute2 iputils-ping curl
```

Պահել system information-ը՝

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

Ստուգել IP addresses-ը՝

```bash
ip addr show
ip addr show | tee ip-addresses.txt
```

Ստուգել routes և default gateway՝

```bash
ip route
ip route | tee routing-table.txt
```

Ստուգել DNS configuration-ը՝

```bash
cat /etc/resolv.conf
cat /etc/resolv.conf | tee dns-config.txt
```

Resolve անել domain name-ը՝

```bash
getent hosts github.com
getent hosts github.com | tee dns-lookup.txt
```

Ստուգել Internet connectivity by IP՝

```bash
ping -c 4 8.8.8.8
ping -c 4 8.8.8.8 | tee internet-ip-test.txt
```

Ստուգել DNS և network connectivity միասին՝

```bash
ping -c 4 github.com
ping -c 4 github.com | tee dns-ping-test.txt
```

Ստուգել HTTPS response headers՝

```bash
curl -I https://github.com
curl -I https://github.com | tee http-test.txt
```

Ստուգել local listening ports՝

```bash
ss -tuln
ss -tuln | tee listening-ports.txt
```

Ստեղծել summary file՝

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

Ստուգել files-ը՝

```bash
ls -la
```

---

## Networking Explanation

Network-ը devices-ի կապ է, որպեսզի դրանք կարողանան data ուղարկել և ստանալ։

Networked devices-ի օրինակներ՝ laptop, phone, router, printer, server, cloud virtual machine, container։

DevOps-ում networking-ը պետք է գրեթե ամեն տեղ՝

* SSH access servers-ին
* web traffic applications-ին
* DNS records domains-ի համար
* Nginx reverse proxy
* database connections
* Docker container communication
* Kubernetes service discovery
* firewall rules
* monitoring endpoints
* cloud networking

Պարզ request-ը հաճախ կախված է մի քանի network layer-ներից։

---

## LAN and WAN

LAN նշանակում է Local Area Network։ Դա սովորաբար օգտագործվում է տան, office-ի կամ local environment-ի ներսում։

Օրինակ LAN՝

```text
Laptop -> Router -> Phone -> Printer
```

WAN նշանակում է Wide Area Network։ WAN-ը միացնում է ավելի մեծ network-ներ։ Internet-ը ամենամեծ public WAN-ն է։

Օրինակ path՝

```text
Laptop -> Home router -> ISP network -> Internet -> Cloud server
```

---

## Client and Server

Client/server model-ը networking-ի ամենակարևոր models-ից մեկն է։

Client-ը request է ուղարկում։ Server-ը ստանում է request-ը և response է վերադարձնում։

Օրինակ՝

```text
Browser  -> request  -> Web server
Browser  <- response <- Web server
```

Երբ բացում ես `https://github.com`, browser-ը client է, իսկ GitHub-ի web infrastructure-ը server side-ն է։

---

## IP Addresses

IP address-ը network-ում device-ի address-ն է։

Օրինակներ՝

```text
192.168.1.25
10.0.0.5
8.8.8.8
```

Private IP addresses-ը օգտագործվում են local network-ի ներսում։ Public IP addresses-ը օգտագործվում են Internet-ում։

Common private IP ranges՝

```text
10.0.0.0/8
172.16.0.0/12
192.168.0.0/16
```

---

## Gateway

Gateway-ը local network-ից դուրս գնալու ելքի կետն է։

Եթե destination-ը local network-ի ներսում չէ, system-ը traffic-ը ուղարկում է default gateway-ի միջոցով։

Linux command՝

```bash
ip route
```

Typical default gateway line՝

```text
default via 192.168.1.1 dev eth0
```

---

## DNS

DNS-ը domain name-ը փոխում է IP address-ի։

Մարդիկ օգտագործում են names՝

```text
github.com
example.com
fashionstation.am
```

Բայց computers-ը network-ում աշխատում են IP addresses-ով։ DNS-ը անում է translation-ը։

Օրինակ՝

```text
github.com -> IP address
```

Linux DNS resolver configuration-ը կարելի է ստուգել՝

```bash
cat /etc/resolv.conf
```

Domain-ը կարելի է resolve անել՝

```bash
getent hosts github.com
```

---

## Ports

Port-ը server-ի վրա կոնկրետ service-ի endpoint է։

Մեկ server-ը կարող է ունենալ մեկ IP address, բայց մի քանի services կարող են լսել տարբեր ports-ի վրա։

Common ports՝

| Service | Port |
| ------- | ---: |
| SSH | 22 |
| DNS | 53 |
| HTTP | 80 |
| HTTPS | 443 |
| PostgreSQL | 5432 |
| MySQL | 3306 |
| Node.js development app | 3000 |

Եթե service-ը expected port-ի վրա չի լսում, clients-ը չեն կարողանա connect լինել, նույնիսկ եթե server-ը reachable է։

---

## Basic Troubleshooting Logic

DevOps troubleshooting chain՝

```text
Domain -> DNS -> IP -> Gateway -> Server -> Port -> Response
```

Useful checks՝

| Problem | Possible Area |
| ------- | ------------- |
| IP ping works, domain ping fails | DNS issue |
| DNS works, HTTPS fails | service, port, firewall, TLS կամ application issue |
| Default route չկա | gateway կամ routing issue |
| Expected port չկա `ss -tuln` output-ում | service-ը կարող է չաշխատել կամ չլսել |

---

## Validation

Run արա այս commands-ը lesson directory-ից՝

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

Expected result՝

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
* networking summary was documented

---

## Quiz Review

| # | Հարց | Ճիշտ պատասխան | Status |
|---:|---|---|---|
| 1 | Ի՞նչ է network-ը | Devices-ի կապ, որպեսզի նրանք data ուղարկեն և ստանան | Passed |
| 2 | Ի՞նչ է LAN-ը | Local Area Network՝ տուն, office կամ local environment | Passed |
| 3 | Ի՞նչ է WAN-ը | Wide Area Network, որը միացնում է մեծ network-ներ | Passed |
| 4 | Browser-ը ինչ դեր ունի `https://github.com` բացելիս | Client | Passed |
| 5 | Server-ը ինչ է անում | Request է ստանում և response վերադարձնում | Passed |
| 6 | IP address-ը ինչի համար է | Device-ը network-ում ճանաչելու համար | Passed |
| 7 | Gateway-ը ինչ դեր ունի | Local network-ից դուրս գնալու ելքն է | Passed |
| 8 | DNS-ը ինչ է անում | Domain name-ը փոխում է IP address-ի | Passed |
| 9 | Port-ը ինչ է նշանակում | Server-ի վրա service-ի door/endpoint | Passed |
| 10 | HTTPS-ի default port-ը | 443 | Passed |
| 11 | SSH-ի default port-ը | 22 | Passed |
| 12 | Եթե IP ping works, բայց domain ping fails | DNS issue | Passed |
| 13 | Default gateway տեսնելու command-ը | `ip route` | Passed |
| 14 | Local listening ports տեսնելու command-ը | `ss -tuln` | Passed |
| 15 | `curl -I https://github.com` ինչ է ստուգում | HTTPS response headers | Passed |

### Quiz Result

```text
Lesson quiz: Passed — 15/15
```

Lesson quiz passed successfully.

---

## Troubleshooting Notes

Եթե IP connectivity-ն աշխատում է, բայց domain connectivity-ն չի աշխատում, ստուգիր DNS-ը՝

```bash
ping -c 4 8.8.8.8
ping -c 4 github.com
cat /etc/resolv.conf
getent hosts github.com
```

Եթե DNS-ը աշխատում է, բայց HTTPS-ը չի աշխատում, ստուգիր service, port, firewall կամ TLS/application behavior՝

```bash
getent hosts github.com
curl -I https://github.com
```

Եթե system-ը չունի default gateway, ստուգիր routes-ը՝

```bash
ip route
```

Եթե local application-ը պետք է լսի port-ի վրա, ստուգիր՝

```bash
ss -tuln
```

---

## Git Workflow

Lesson-ը ավարտելուց և quiz-ը անցնելուց հետո աշխատանքը պահվելու է Git-ով՝

```bash
cd ~/devops-labs
git status
git add README.md ROADMAP.md 02-networking-ccna-foundations
git commit -m "Complete networking basics lesson"
git push
git status
```

Expected final result՝

```text
nothing to commit, working tree clean
```

---

## What I Learned

Այս դասում ես սովորեցի DevOps-ի համար անհրաժեշտ networking basics-ը։

Ես սովորեցի՝ ինչպես LAN, WAN, clients, servers, IP addresses, gateways, DNS և ports միասին աշխատում են, երբ request-ը computer-ից հասնում է server-ին։

Ես նաև գործնականում փորձեցի Linux networking inspection commands և սովորեցի basic troubleshooting flow՝ DNS, connectivity, routes, gateway, ports և services ստուգելու համար։

---

## Status

Lesson completed, quiz passed, ready to commit and push.
