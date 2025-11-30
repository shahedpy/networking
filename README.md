# Networking

## Syllabus
* Classless addressing, NAT, Internet Assigned Numbers Authority (IANA), ISP roles
* Anatomy of IPV4 address, The subnet mask, Subnetting: Basic Terminology, Subnetting a subnet or VLSM
* Network Security: Asymmetric key cryptography, Public key cryptography (RSA), Practice problems in RSA 
* Routing Protocols: Popular routing algorithms and metric, Flooding technique, The distance vector routing (DVR) protocol, Link-state routing 
* RIP and its drawback, Border gateway protocol (BGP), Wireless Networking, RTS/CTS protocols, Address resolution protocol (ARP) Reverse Address Resolution Protocol (RARP) Dynamic Host Configuration Protocol (DHCP)
* Mobile Networks: Wi-Fi & Wi-max architecture, Final Exam Review Class

## Internet Protocol (IP)

- The Internet Protocol is the cornerstone of the TCP/IP architecture. All computers on the Internet understand IP.

### Main tasks of IP

- Addressing: assigning unique addresses to hosts.
- Fragmentation: splitting packets when necessary.

### IP versions

- **Internet Protocol version 4 (IPv4):** currently used version of Internet Protocol.
- **Internet Protocol version 6 (IPv6):** the upcoming replacement for IPv4. It contains some major improvements and new features.

### IPv4 basics

An IPv4 address is a 32-bit number that identifies a network interface on the Internet (for example, a computer or a router).
- Connectionless protocol (best-effort delivery)
- Supports packet fragmentation when necessary
- Addressing via 32-bit Internet addresses
- IP does not provide end-to-end message reliability or flow control; it performs best-effort delivery and does not guarantee packet delivery. Higher-layer protocols like TCP provide reliability and flow control.

### IP address types

- **Public address:** An address assigned by an Internet Service Provider (ISP) and is globally routable and unique.
- **Private address:** An address assigned to a device on a private TCP/IP local network (e.g., RFC 1918 ranges); these are not routable on the public Internet.

### IPv6

- Maintains good features of IPv4, discards bad ones.
- Not compatible with IPv4.
- Compatible with all other Internet protocols including TCP, UDP, ICMP, DNS, etc.

#### Main features:

- Long addresses (128 bits) => supports billions of hosts.
- Simplified, fixed size header=> routers can process packets faster.
- Support for authentication and privacy
- Better support for type of service.

### IP Address Structure
Each network interface connected to the Internet has a unique address consisting of two parts:
 - **Network address:** address of the network within the Internet (used by gateways for routing IP packets between networks).
 - **Host address:** address of the computer within the network (used for delivering packets to a particular network interface within the network).

- The 32-bit IP address is separated into four 8-bit octets, allowing each octet to have a value ranging from 0 to 255.
- Furthermore, the IP address is logically separated into two distinct components: the network ID and the host ID. The network ID is used to identify the subnet upon which the host resides. The host ID is used to identify the host itself within the given subnet.

### Classes of IP addresses
- Different networks have different sizes. Basically, there are many small networks and few large networks.
- To provide efficient use of 32-bit address space, IPv4 defined several address classes and associated address formats:
 - **Class A:** allows 128 networks, 16 million hosts each. The IP address start from 1.0.0.0 to 127.255.255.255, and tbe mask address is 255.0.0.0
 - **Class B:** allows 16,382 networks, 65,534 hosts each. The IP address start from 128.0.0.0 to 191.255.255.255, and the mask address is 255.255.0.0
 - **Class C:** allows 2 million networks, 254 hosts each. The IP address start from 192.0.0.0 to 223.255.255.255, and the mask address is 255.255.255.0
 - **Class D:** multicast networks. The IP address start from 224.0.0.0 to 239.255.255.255.
 - **Class E:** reserved for future use. From 240 to 255 and the 255.255.255.255 used for broadcast to all the subnet.

|Class |Byte 1    | Byte 2   | Byte 3  | Byte 4  |
|------|----------|----------|---------|---------|
|A     | Net ID   | Host ID  | Host ID | Host ID |
|B     | Net ID   | Net ID   | Host ID | Host ID |
|C     | Net ID   | Net ID   | Net ID  | Host ID |
|D     | Multicast Address                       |
|E     | Reserved for future use                 |


### Strategies to Conserve Addresses
- Several strategies have been developed and implemented to help the Internet community on how provides a good managing of IP addresses. These strategies help reduce the load on Internet routers and help administrators use globally unique IP addresses more efficiently. There are two common strategies, which are:
- Private Addressing
- Classless Inter-Domain Routing (CIDR)

#### Private Addressing
- It means if the internetwork is limited to one organization, the IP addresses need only be unique within that organization. Only networks that interface with public networks such as the Internet need public addresses. Using public addresses on the outside and private addresses for inside networks is very effective.
Private Addresses:
RFC1918 designates three ranges of IP addresses as private:
- 10.0.0.0 through 10.255.255.255
- 172.16.0.0 through 172.31.255.255
- 192.168.0.0 through 192.168.255.255

|Address Block                  | Classfull Equivalent                         | Prefix Length | Number of Addresses |
|-------------------------------|----------------------------------------------|---------------|---------------------|
| 10.0.0.0 - 10.255.255.255     | 1 Class A <br> 256 Class B <br> 65,536 Class C   | /8            | 16,777,216          |
| 172.16.0.0 - 172.31.255.255   | 16 Class B <br> 4,096 Class C                  | /12           | 1,048,576           |
| 192.168.0.0 - 192.168.255.255 | 1 Class B <br> 256 Class C                     | /16           | 65,536              |

There are two ways to convert the private address to public address:
1. Network Address Translation (NAT).
This technique has been used to convert the private address to public address, the NAT allowing us to access the internet and get services. The basic idea, is that technique used pool of public addresses and assign for each private address one public address. Thus, this way is inefficient due to the fact, that there are cost and delay associated with this operation. The table and the figure below show how the NAT make the mapping.


2. Port Address Translation (PAT).
It's another technique used to convert the private address to public. During PAT, each computer on LAN is translated 10 the same [P addre.ss (public), but with a different port number assignment. This way is much better than the NAT because we can use one public address to translate any private address, therefore we saved the cost. The table below shows the process of the PAT


### Classless Inter-Domain Routing (CIDR)
- Classless Inter Domain Routing (CIDR) is a method for assigning IP addresses without using the standard IP address classes Like Class A, Class B or Class C. In CIDR , an IP address is represented as A.B.C.D /n, where "/n" is called the IP prefix or network prefix. The IP prefix identifies the number of significant bits used to identify a network.
- Example, 192.9.205.22 /18 means, the first 18 bits are used to represent the network and the remaining 14 bits are used to identify hosts.
- It's-basically the method that ISPs (Internet Service Providers) use to allocate an amount of addresses to a company, a home -- a customer. They provide addresses in a certain block size
- When you receive a block of addresses from an ISP, what you get will look something like this: 192.168.10.32/28. This is telling you what your subnet mask is. The slash notation (/) means how many bits are turned on (1s).

The Class A default subnet mask, which is 255.0.0.0. This means that the first byte of the subnet mask is all ones (1s), or 11111111. When referring to a slash notation, you need to count all the 1s bits to figure out your mask. The 255.0.0.0 is considered a /8 because  it has 8 bits that are 1s-that is, 8 bits that are turned on

In a Class C address, only 8 bits are available for defining the hosts
that subnet bits start at the left and go to the right without skipping bits. This means that the only Class C subnet masks can be the following:

| Binary              | Decimal        | CIDR |
|---------------------|----------------|------|
| 10000000            | 128            | /25  |
| 11000000            | 192            | /26  |
| 11100000            | 224            | /27  |
| 11110000            | 240            | /28  |
| 11111000            | 248            | /29  |
| 11111100            | 252            | /30  |

