
# Networking

An overview of the Internet Protocol (IP), addressing, and common strategies for conserving IPv4 address space.

## Table of contents

- [Internet Protocol (IP)](#internet-protocol-ip)
- [IPv4 Basics](#ipv4-basics)
- [Address Types](#address-types)
- [IPv6](#ipv6)
- [IP Address Structure](#ip-address-structure)
- [Classes of IP Addresses](#classes-of-ip-addresses)
- [Strategies to Conserve Addresses](#strategies-to-conserve-addresses)
- [Internet number governance (IANA & RIRs)](#internet-number-governance-iana--rirs)
- [ISP roles](#isp-roles)
- [Classless Inter-Domain Routing (CIDR)](#classless-inter-domain-routing-cidr)

## Internet Protocol (IP)

The Internet Protocol is the cornerstone of the TCP/IP architecture. It is a connectionless, best-effort protocol used to deliver packets between hosts on different networks.

### Main tasks of IP

- Addressing — assigning unique addresses to hosts.
- Fragmentation — splitting packets when necessary to traverse smaller MTUs.

### IP versions

- **IPv4** — the widely deployed IP version (32-bit addresses).
- **IPv6** — the successor to IPv4 (128-bit addresses) with improvements in address space and header design.

## IPv4 basics

An IPv4 address is a 32-bit number that identifies a network interface (for example, a computer or a router).

- Connectionless protocol (best-effort delivery).
- Supports packet fragmentation when necessary.
- Uses 32-bit Internet addresses.
- IP does not provide end-to-end reliability or flow control; higher-layer protocols such as TCP provide those features.

## Address types

- **Public address:** Assigned by an ISP; globally routable and unique.
- **Private address:** Used within private networks (RFC 1918); not routable on the public Internet.

## IPv6

- Uses 128-bit addresses (vastly larger address space).
- Simplified fixed-size header improves routing performance.
- Provides better support for authentication, privacy, and quality of service.
- IPv6 is not directly compatible with IPv4; transition mechanisms are used during migration.

## IP Address Structure

Each IP address typically consists of two logical parts:

- **Network portion:** identifies the network (used by routers for forwarding).
- **Host portion:** identifies the host/interface within that network.

IPv4 addresses are commonly written as four decimal octets (0–255), e.g. `192.0.2.1`.

## Classes of IP addresses (historical)

> Note: Classful addressing is largely obsolete, retained here for historical context.

- **Class A:** 1.0.0.0 — 127.255.255.255 (default mask: `255.0.0.0`, `/8`).
- **Class B:** 128.0.0.0 — 191.255.255.255 (default mask: `255.255.0.0`, `/16`).
- **Class C:** 192.0.0.0 — 223.255.255.255 (default mask: `255.255.255.0`, `/24`).
- **Class D:** 224.0.0.0 — 239.255.255.255 (multicast).
- **Class E:** 240.0.0.0 — 255.255.255.255 (reserved).

Classful layout by octet:

| Class | Byte 1 | Byte 2 | Byte 3 | Byte 4 |
|-------|--------|--------|--------|--------|
| A     | Net ID | Host   | Host   | Host   |
| B     | Net ID | Net ID | Host   | Host   |
| C     | Net ID | Net ID | Net ID | Host   |
| D     | Multicast (address group)               |
| E     | Reserved                                |

## Strategies to Conserve Addresses

To reduce pressure on the IPv4 address space, several strategies are used:

- **Private addressing (RFC 1918)** — use private ranges inside organizations and map to public addresses at network edges.
- **CIDR (Classless Inter-Domain Routing)** — allocate and route blocks by arbitrary prefix lengths instead of fixed classes.

### Private addressing (RFC 1918)

Private address ranges designated by RFC 1918:

- `10.0.0.0/8` (10.0.0.0 — 10.255.255.255)
- `172.16.0.0/12` (172.16.0.0 — 172.31.255.255)
- `192.168.0.0/16` (192.168.0.0 — 192.168.255.255)

Summary table:

| Address Block | Classful Equivalent | Prefix Length | Number of Addresses |
|---------------:|--------------------:|:-------------:|--------------------:|
| `10.0.0.0/8`    | 1 Class A           | `/8`          | 16,777,216          |
| `172.16.0.0/12` | 16 Class B          | `/12`         | 1,048,576           |
| `192.168.0.0/16`| 1 Class B           | `/16`         | 65,536              |

### Address translation: NAT and PAT

- **Network Address Translation (NAT):** maps private addresses to public addresses using a pool of public IPs. Basic NAT mappings can be 1:1 (private:public).
- **Port Address Translation (PAT) / NAT overload:** maps many private addresses to a single public IP using distinct source ports; this conserves public IPs and is the common form of NAT used in home routers.

## Classless Inter-Domain Routing (CIDR)

CIDR represents addresses as `A.B.C.D/N` where `/N` is the prefix length (number of network bits). For example, `192.9.205.22/18` means the first 18 bits identify the network and the remaining 14 bits identify hosts.

CIDR allows flexible block sizes (e.g., `/28`, `/27`, `/24`) and is used extensively by ISPs to allocate address space.

Subnet mask and CIDR examples (common Class C-style subnets):

| Binary       | Decimal | CIDR |
|--------------|--------:|:----:|
| `10000000`   | 128     | `/25`|
| `11000000`   | 192     | `/26`|
| `11100000`   | 224     | `/27`|
| `11110000`   | 240     | `/28`|
| `11111000`   | 248     | `/29`|
| `11111100`   | 252     | `/30`|

## Internet number governance (IANA & RIRs)

The Internet Assigned Numbers Authority (IANA) manages global coordination for the assignment of IP address blocks, autonomous system (AS) numbers, and other protocol parameters.

- IANA allocates large blocks of addresses and ASNs to Regional Internet Registries (RIRs) such as ARIN, RIPE NCC, APNIC, AFRINIC, and LACNIC.
- RIRs allocate smaller blocks to Internet Service Providers (ISPs) and sometimes directly to large organizations.
- This hierarchical model ensures global uniqueness and coordinated routing of Internet address space.

See: https://www.iana.org and the RIRs' websites for regional policies and allocations.

## ISP roles

Internet Service Providers (ISPs) play several important roles in the IP addressing ecosystem and in general Internet connectivity:

- Allocation and assignment — ISPs receive address blocks from RIRs and assign public addresses to customers (either dynamically via DHCP or as static assignments).
- Routing and peering — ISPs announce IP prefixes via routing protocols (e.g., BGP) and establish peering or transit agreements to exchange traffic.
- NAT and address conservation — Many ISPs use NAT/PAT at customer premises or within their networks to conserve public address space.
- Core services — ISPs often provide DNS resolvers, DHCP servers, and other gateway services for customers, and help with IPv6 migration.

These roles make ISPs a critical point of contact for both address allocation and operational support on the public Internet.

