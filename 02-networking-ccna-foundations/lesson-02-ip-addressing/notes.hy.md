# Lesson 02 — IP Addressing

![Status](https://img.shields.io/badge/status-completed-brightgreen)
![Focus](https://img.shields.io/badge/focus-IP%20addressing-blue)
![Level](https://img.shields.io/badge/level-foundation-lightgrey)

---

## Overview

Այս դասը բացատրում է IPv4 addressing-ը DevOps troubleshooting-ի տեսանկյունից։

IP addressing-ը networking-ի ամենակարևոր հիմքերից է, որովհետև յուրաքանչյուր server, cloud VM, container, router և service network-ում աշխատելու համար address է օգտագործում։

Այս դասում ես սովորեցի հասկանալ IPv4 address-ի format-ը, տարբերել private և public IP addresses-ը, հասկանալ CIDR notation-ը, subnet mask-ի basic իմաստը, default gateway-ը, loopback-ը և `localhost`-ը։ Նաև սովորեցի Linux commands-ով ստուգել IP addressing information-ը և պահել outputs-ը portfolio documentation-ի համար։

---

## Learning Objectives

Այս դասից հետո ես սովորեցի՝

* ինչ է IP address-ը
* ինչ format ունի IPv4 address-ը
* ինչպես տարբերել valid և invalid IPv4 addresses
* որոնք են private IP ranges-ը
* ինչ տարբերություն կա private և public IP-ի միջև
* ինչ է NAT-ը basic մակարդակով
* ինչ է subnet mask-ը
* ինչ է CIDR notation-ը, օրինակ՝ `/24`
* ինչ է նշանակում `0.0.0.0/0`
* ինչ դեր ունի gateway-ը
* ինչ է loopback address-ը
* ինչ է `localhost`-ը
* ինչպես Linux-ում ստուգել IP addresses, routes և gateway
* ինչպես command output-ը պահել documentation-ի համար
* ինչպես IP addressing-ը կապել DevOps troubleshooting-ի հետ

---

## Key Concepts

| Concept | Բացատրություն |
| ------- | ------------- |
| IP address | Network-ում device-ի հասցե |
| IPv4 | Չորս octet-ով IP format, օրինակ՝ `192.168.1.25` |
| Octet | IPv4-ի մեկ մաս, որի արժեքը կարող է լինել `0`-ից `255` |
| Private IP | Private/local network-ում օգտագործվող IP |
| Public IP | Internet-ում օգտագործվող IP |
| NAT | Private և public addressing-ի միջև translation |
| Subnet mask | Ցույց է տալիս IP-ի network part-ը և host part-ը |
| CIDR | Կարճ prefix notation, օրինակ՝ `/24` |
| `0.0.0.0/0` | Բոլոր IPv4 addresses-ը / ամբողջ Internet-ը |
| Gateway | Դուրս գնալու exit point դեպի այլ network-ներ |
| Loopback | Local machine-ի internal network interface |
| `localhost` | Local machine-ին ցույց տվող hostname |

---

## Commands Learned

| Command | Նպատակ | Օրինակ |
| ------- | ------ | ------ |
| `ip -4 addr show` | Ցույց է տալիս IPv4 addresses-ը | `ip -4 addr show` |
| `hostname -I` | Արագ ցույց է տալիս IP addresses-ը | `hostname -I` |
| `ip route` | Ցույց է տալիս routing table և gateway | `ip route` |
| `grep default` | Ֆիլտրում է default route-ը | `ip route \| grep default` |
| `awk` | Output-ից field է վերցնում | `awk '/default/ {print $3; exit}'` |
| `ping` | Ստուգում է connectivity | `ping -c 4 127.0.0.1` |
| `ip addr show lo` | Ցույց է տալիս loopback interface-ը | `ip addr show lo` |
| `getent hosts localhost` | Resolve է անում localhost-ը | `getent hosts localhost` |
| `tee` | Output-ը ցույց է տալիս և պահում file-ի մեջ | `command \| tee file.txt` |

---

## Lab Structure

Այս lab-ը օգտագործում է հետևյալ folder-ը՝

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

Ստեղծել lesson directory՝

```bash
cd ~/devops-labs
mkdir -p 02-networking-ccna-foundations/lesson-02-ip-addressing
cd 02-networking-ccna-foundations/lesson-02-ip-addressing
pwd
```

Տեսնել IPv4 addresses-ը՝

```bash
ip -4 addr show
```

Պահել IPv4 address information-ը՝

```bash
ip -4 addr show | tee ipv4-addresses.txt
```

Արագ տեսնել machine-ի IP addresses-ը՝

```bash
hostname -I
```

Պահել quick IP output-ը՝

```bash
hostname -I | tee hostname-ip.txt
```

Տեսնել routing table-ը՝

```bash
ip route
```

Պահել routing table-ը՝

```bash
ip route | tee routing-table.txt
```

Պահել default route-ը՝

```bash
ip route | grep default | tee default-gateway.txt
```

Gateway IP-ն պահել variable-ի մեջ՝

```bash
GATEWAY_IP=$(ip route | awk '/default/ {print $3; exit}')
echo "Gateway IP: $GATEWAY_IP"
```

Պահել gateway IP-ն՝

```bash
echo "Gateway IP: $GATEWAY_IP" | tee gateway-ip.txt
```

Ping անել gateway-ին՝

```bash
ping -c 4 "$GATEWAY_IP"
```

Պահել gateway ping test-ը՝

```bash
ping -c 4 "$GATEWAY_IP" | tee gateway-ping-test.txt
```

Տեսնել loopback interface-ը՝

```bash
ip addr show lo
```

Պահել loopback interface output-ը՝

```bash
ip addr show lo | tee loopback-interface.txt
```

Ping անել loopback address-ին՝

```bash
ping -c 4 127.0.0.1
```

Պահել loopback ping output-ը՝

```bash
ping -c 4 127.0.0.1 | tee loopback-ping-test.txt
```

Resolve անել `localhost`-ը՝

```bash
getent hosts localhost
```

Պահել localhost lookup-ը՝

```bash
getent hosts localhost | tee localhost-lookup.txt
```

Ստեղծել IP addressing summary՝

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

Ստուգել folder-ի content-ը՝

```bash
ls -la
```

Ստուգել repository status-ը՝

```bash
cd ~/devops-labs
git status
```

---

## IPv4 Explanation

IPv4 address-ը գրվում է չորս թվերով, որոնք բաժանված են կետերով։

Օրինակ՝

```text
192.168.1.25
```

Յուրաքանչյուր մաս կոչվում է octet։

```text
192 . 168 . 1 . 25
```

Յուրաքանչյուր octet պետք է լինի `0`-ից `255`։

Ճիշտ օրինակներ՝

```text
192.168.1.10
10.0.0.5
172.16.20.30
8.8.8.8
```

Սխալ օրինակ՝

```text
192.168.1.300
```

Սա սխալ է, որովհետև `300`-ը մեծ է `255`-ից։

---

## Private IP Addresses

Private IP addresses-ը օգտագործվում են private networks-ում՝ տուն, office, internal cloud network, Docker network, lab environment։

Private IP ranges՝

```text
10.0.0.0/8
172.16.0.0/12
192.168.0.0/16
```

Common examples՝

```text
192.168.1.10
10.0.1.20
172.17.0.2
```

Private IP-ները direct public Internet-ից հասանելի չեն առանց routing, NAT, VPN, load balancer կամ public mapping-ի։

---

## Public IP Addresses

Public IP address-ը օգտագործվում է Internet-ում։

Cloud VM-ը կարող է ունենալ public IP, որ admin-ը կարողանա SSH անել կամ service-ը expose անել HTTP/HTTPS-ով։

Պարզ model՝

```text
Laptop private IP: 192.168.1.25
Router public IP:  89.x.x.x
Cloud VM public IP: 34.x.x.x
```

DevOps Engineer-ը պետք է կարողանա հասկանալ՝ որ IP-ն է internal, որը՝ externally reachable։

---

## NAT Basics

NAT նշանակում է Network Address Translation։

Այն թույլ է տալիս private devices-ին դուրս գալ Internet public IP-ի միջոցով։

Օրինակ՝

```text
Laptop: 192.168.1.10
Phone:  192.168.1.11
TV:     192.168.1.12
```

Այս devices-ը կարող են դուրս գալ Internet նույն router public IP-ով։

```text
Router public IP: 89.x.x.x
```

NAT-ը կարևոր է home networks-ում, cloud networking-ում, Docker networking-ում և Kubernetes networking-ում։

---

## Subnet Mask

Subnet mask-ը առանձնացնում է IP address-ի network part-ը և host part-ը։

Օրինակ՝

```text
IP:          192.168.1.25
Subnet mask: 255.255.255.0
```

Beginner-friendly ձևով՝

```text
Network part: 192.168.1
Host part:    25
```

Նույն `/24` network-ում devices-ը հաճախ ունեն նույն առաջին երեք octet-ը։

Նույն network՝

```text
192.168.1.10
192.168.1.25
192.168.1.100
```

Ուրիշ network՝

```text
192.168.2.25
```

---

## CIDR Notation

CIDR-ը network prefix information-ը գրելու կարճ ձև է։

Օրինակ՝

```text
192.168.1.25/24
```

`/24` նշանակում է՝ առաջին 24 bits-ը network prefix են։

Պարզ իմաստով՝

```text
Network: 192.168.1.0
Hosts:   192.168.1.x
```

Common examples՝

| CIDR | Subnet mask | Իմաստ |
| ---- | ----------- | ----- |
| `/8` | `255.0.0.0` | Մեծ network |
| `/16` | `255.255.0.0` | Մեծ private/cloud network |
| `/24` | `255.255.255.0` | Սովորական փոքր LAN subnet |
| `/32` | `255.255.255.255` | Մեկ կոնկրետ IP address |

---

## `0.0.0.0/0` Explanation

`0.0.0.0/0` նշանակում է բոլոր IPv4 addresses-ը։

Firewall կամ cloud security rules-ում դա նշանակում է anywhere on the Internet։

Օրինակ՝

```text
SSH port 22 open to 0.0.0.0/0
```

Սա նշանակում է, որ SSH-ը բաց է ամբողջ Internet-ին։

Production systems-ում սա հաճախ unsafe է։ SSH access-ը սովորաբար պետք է սահմանափակել trusted IP addresses-ով, VPN-ով, bastion host-ով կամ controlled access pattern-ներով։

---

## Gateway

Gateway-ը exit point է, որի միջոցով machine-ը հասնում է ուրիշ network-ների։

Օրինակ՝

```text
Your IP: 192.168.1.25
Gateway: 192.168.1.1
```

Եթե destination-ը local network-ում չէ, system-ը traffic-ը ուղարկում է gateway-ին։

```text
Laptop → Gateway/Router → Internet → Server
```

Linux command՝

```bash
ip route
```

Typical output՝

```text
default via 192.168.1.1 dev eth0
```

`default via` նշանակում է default gateway։

---

## Loopback and Localhost

Loopback address-ը ցույց է տալիս local machine-ին։

```text
127.0.0.1
```

`localhost` սովորաբար resolve է լինում local machine-ին։

```text
localhost → 127.0.0.1
```

Երբ application-ը աշխատում է local machine-ի վրա, այն հաճախ բացում ենք այսպես՝

```text
http://localhost:3000
http://127.0.0.1:3000
```

Սա շատ է օգտագործվում local development-ում, Docker-ում, Nginx reverse proxy testing-ում, systemd service validation-ում և Kubernetes port-forward-ում։

---

## DevOps Troubleshooting Examples

### IP կա, բայց gateway չկա

Եթե `ip -4 addr show` IP ցույց է տալիս, բայց `ip route`-ում չկա `default via`, system-ը կարող է local network-ում լինել, բայց չկարողանալ դուրս գալ ուրիշ network կամ Internet։

### Private IP չի նշանակում public access

Եթե server-ը ունի միայն private IP, օրինակ՝ `10.0.1.10`, դա սովորաբար direct Internet-ից reachable չէ։

Կարող է պետք լինել՝

* public IP
* NAT
* VPN
* load balancer
* bastion host
* routing rule
* firewall rule

### SSH open է ամբողջ աշխարհին

Եթե SSH-ը բաց է `0.0.0.0/0`-ի համար, այն reachable է ամբողջ Internet-ից։

Սա production-ի համար risky է և պետք է սահմանափակել։

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

| Սխալ | Խնդիր | Ճիշտ մոտեցում |
| ---- | ----- | ------------- |
| Կարծել, որ ամեն IP public է | Private IP-ները direct Internet reachable չեն | Տարբերել private և public IP-ները |
| `/24`-ը շփոթել port-ի հետ | `/24` network prefix length է | Ports-ը CIDR-ից առանձին concept են |
| SSH-ը բացել `0.0.0.0/0`-ին | SSH-ը հասանելի է ամբողջ աշխարհից | Սահմանափակել trusted IP-ներով |
| Gateway-ը չստուգել | Default gateway չլինելը կարող է կոտրել Internet access-ը | Ստուգել `ip route` |
| `localhost`-ը շփոթել remote server-ի հետ | `localhost` local machine-ն է | Օգտագործել ճիշտ remote IP կամ domain |

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

Սխալ տրված պատասխանը ուղղվեց՝

```text
192.168.1.25/24
```

`/24` նշանակում է network prefix length, ոչ թե SSH port։

---

## Git Workflow

Այս lesson documentation-ը repository-ում տեղադրելուց հետո օգտագործել specific paths՝

```bash
cd ~/devops-labs

git status

git add README.md ROADMAP.md 02-networking-ccna-foundations/README.md 02-networking-ccna-foundations/lesson-02-ip-addressing

git commit -m "Complete IP addressing lesson"

git push

git status
```

Expected final result՝

```text
nothing to commit, working tree clean
```

---

## What I Learned

Այս դասում ես սովորեցի IP addressing-ի հիմքերը DevOps-ի համար։ Ես հասկացա private և public IP-ների տարբերությունը, CIDR notation-ը, gateway-ի դերը, loopback/localhost concepts-ը և ինչպես այս ամենը օգտագործել troubleshooting-ի ժամանակ։

---

## Final Status

Lesson completed, quiz passed, committed and pushed to GitHub.
