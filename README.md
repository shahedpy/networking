# Networking

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
