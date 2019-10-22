---

copyright:

  years: 2019

lastupdated: "2019-10-14"

keywords: dns, dns-svcs, DNS Services, Private DNS, dns vpc, Access Control Lists, permitted networks

subcollection: dns-svcs

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:DomainName: data-hd-keyref="DomainName"}
{:note: .note}
{:tip: .tip}
{:important: .important}
{:deprecated: .deprecated}
{:generic: data-hd-programlang="generic"}



# DNS Concepts
{: #dns-concepts}

{{site.data.keyword.cloud}} DNS Services is in Experimental Release. At this time the service is available to whitelisted customers only.
{: important}

This document contains some concepts and definitions related to the internet's domain name system (DNS) and how it affects your usage of DNS services


## DNS Zones
{: #what-is-zone}

A DNS zone is a collection of resource records which belongs to a single parent instance. All resource records have the zone's domain name as a suffix. You can create, update, delete, get, and list the DNS Zones using curl commands.

See [Manage DNS zones](/docs/dns-svcs?topic=dns-svcs-managing-dns-zones) for more information on how to manage DNS zones.

IBM Cloud DNS Services permits only two level zones to be added. For instance, `example.com` is allowed, while `subdomain.example.com` is not. However, subdomains can be defined within an added zone (for example, `subdomain.example.com`, `hostname.example.com`, or `hostname.subdomain.example.com` are all valid names within the zone `example.com`).

## Permitted networks
{: #permitted-networks}

Permitted networks are the VPCs that are allowed to perform name resolution on the DNS Zone. The permitted network is used as an access control mechanism to guarantee that only the VPC that has been added as a permitted network is allowed to perform name resolution on the DNS zone.

See [Managing permitted networks](/docs/dns-svcs?topic=dns-svcs-managing-permitted-networks) for more information on how to manage permitted networks.

## Resource Records (RR)
{: #what-are-resource-records}

Resource Records(RR) are entries in the DNS Zone files. The most common type is an A record that provides a mapping between a name to an IPv4 address.

### Supported Resource Record Types
{: #supported-resource-record-types}

DNS Services supports the following types of Resource Records:

#### A (IPv4 Address Record)
{: #record-type-a}

Provides a mapping of a host to an IPv4 address.

#### AAAA (IPv6 Address Record)
{: #record-type-quad-a}

Provides a mapping of a host to an IPv6 address.

#### CNAME (Canonical Name)
{: #record-type-cname}
Provides a way to alias a hostname to another hostname or Canonical Name (CNAME).

#### PTR (Pointer)
{: #record-type-pointer}

Enables reverse DNS lookup, from an IP address to a hostname. The IP address can be an IPv4 address or IPv6 address.

#### MX (Mail Exchange)
{: #record-type-mx}

This record specifies the SMTP mail server for the DNS zone.

#### SRV (Service Location)
{: #record-type-srv}

This record specifies the location of the server(s) for a specific protocol and domain.

#### TXT (Text)
{: #record-type-tx}

This record is used to hold descriptive text for a given name.

#### NS (Name Server)
{: #record-type-ns}

This type of record cannot be created in DNS zone but can be queried for your DNS zone. The data returned is statically defined and cannot be changed.

#### SOA (Start of Authority)
{: #record-type-soa}

This type of record cannot be created in DNS Zone but can be queried for your DNS zone. The data returned is statically defined and cannot be changed.
