# Section 9: Route 53

## 87. What is a DNS?

- Domain Name System which translates the human friendly hostnames into the machine IP addresses
- www.google.com => 172.217.18.36
- DNS is the backbone of the Internet
- DNS uses hierarchical naming structure

com
example.com
www.example.com
api.example.com

DNS Terminologies

- Domain Registrar: Amazon Route 53, GoDaddy, ...
- DNS Records: A, AAAA, CNAME, NS, ...
- Zone File: contains DNS records
- Name Server: resolves DNS queries (Authoritative or Non-Authoritative)
- Top Level Domain (TLD): .com, .us, .in, .gov, .org, ...
- Second Level Domain (SLD): amazon.com, google.com, ...

http://api.www.example.com.

        http:// - Protocol
        api. = FQDN (Fully Qualified Domain Name)
        www. = Sub Domain
        example. = SLD
        .com = TLD
        . = Root

## 88. Route 53 Overview

Amazon Route 53

- A highly available, scalable, fully managed and Authoritative DNS

  - Authoritative = the customer (you) can update the DNS records

- Route 53 is also a Domain Registrar

- Ability to check the health of your resources

- The only AWS service which provides 100% availability SLA

- Why Route 53? 53 is a reference to the traditional DNS port
