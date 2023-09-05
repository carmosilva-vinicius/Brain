# Privacy and Security

The DNS protocol is unencrypted and does not account for confidentiality, integrity or authentication, so if you use an untrusted network or a malicious ISP, your DNS queries can be eavesdropped and the responses [manipulated](https://en.wikipedia.org/wiki/Man-in-the-middle_attack "wikipedia:Man-in-the-middle attack"). Furthermore, DNS servers can conduct [DNS hijacking](https://en.wikipedia.org/wiki/DNS_hijacking "wikipedia:DNS hijacking").

You need to trust your DNS server to treat your queries confidentially. DNS servers are provided by ISPs and [third-parties](https://wiki.archlinux.org/title/Domain_name_resolution#Third-party_DNS_services). Alternatively you can run your own [recursive name server](https://wiki.archlinux.org/title/Domain_name_resolution#DNS_servers), which however takes more effort. If you use a [DHCP](https://wiki.archlinux.org/title/DHCP "DHCP") client in untrusted networks, be sure to set static name servers to avoid using and being subject to arbitrary DNS servers. To secure your communication with a remote DNS server you can use an encrypted protocol, like [DNS over TLS](https://en.wikipedia.org/wiki/DNS_over_TLS "wikipedia:DNS over TLS") ([RFC 7858](https://tools.ietf.org/html/rfc7858 "rfc:7858")), [DNS over HTTPS](https://en.wikipedia.org/wiki/DNS_over_HTTPS "wikipedia:DNS over HTTPS") ([RFC 8484](https://tools.ietf.org/html/rfc8484 "rfc:8484")), or [DNSCrypt](https://en.wikipedia.org/wiki/DNSCrypt "wikipedia:DNSCrypt"), provided that both the upstream server and your [resolver](https://wiki.archlinux.org/title/Domain_name_resolution#DNS_servers) support the protocol. An alternative can be a dedicated software to encrypt and decrypt the communication, such as [stunnel](https://wiki.archlinux.org/title/Stunnel "Stunnel"). To verify that responses are actually from [authoritative name servers](https://en.wikipedia.org/wiki/Authoritative_name_server "wikipedia:Authoritative name server"), you can validate [DNSSEC](https://wiki.archlinux.org/title/DNSSEC "DNSSEC"), provided that both the upstream server(s) and your [resolver](https://wiki.archlinux.org/title/Domain_name_resolution#DNS_servers) support it.

Although one may use an encrypted DNS resolver, the browser still leaks the domain names in the [Server Name Indication](https://en.wikipedia.org/wiki/Server_Name_Indication "wikipedia:Server Name Indication") when requesting the website certificate. This leak can be checked using the [Wireshark](https://wiki.archlinux.org/title/Wireshark "Wireshark") filter `tls.handshake.extensions_server_name_len > 0`, or using the command line below. A proposed solution is to use the [Encrypted Client Hello (ECH)](https://en.wikipedia.org/wiki/Server_Name_Indication#Encrypted_Client_Hello "wikipedia:Server Name Indication"), a TLS 1.3 protocol extension.

Source: https://wiki.archlinux.org/title/Domain_name_resolution#Privacy_and_security

DoT can be configured through [[Systemd#Configuring DoT ( DNS over TLS) using Systemd|systemd]].





