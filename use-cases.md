---

copyright:
  years: 2019
lastupdated: "2019-12-03"

keywords: dns-svcs, DNS Services, Private DNS

subcollection: dns-svcs

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:external: target="_blank" .external}
{:DomainName: data-hd-keyref="DomainName"}
{:note: .note}
{:tip: .tip}
{:important: .important}
{:deprecated: .deprecated}
{:generic: data-hd-programlang="generic"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:download: .download}

# Use cases
{: #use-cases}

{{site.data.keyword.dns_full_notm}} is in Experimental Release. At this time the service is available to whitelisted customers only.
{: important}

This section covers some possible use cases you might have while using {{site.data.keyword.dns_full}}.
{:shortdesc}

## Using {{site.data.keyword.dns_short}} for VPC
{: #using-dns-services-for-vpc}

  1. Create a VPC instance.
  2. Create a {{site.data.keyword.dns_short}} instance.
  3. Add a DNS zone to the {{site.data.keyword.dns_short}} instance.
  4. Designate the VPC instance as a permitted network for the DNS zone.
  5. Add a DNS Resource Record to the DNS zone.
  6. Configure VPC servers to use {{site.data.keyword.dns_short}} resolvers.
  7. Verify name resolution of the DNS Resource Record works from within the VPC.


## Creating multiple zones with duplicate names
{: #creating-multiple-zones-with-duplicate-names}

  1. Create an instance of {{site.data.keyword.dns_short}}.
  2. Create a DNS zone for each environment (for example, production, staging, development, testing). When creating the zone, be sure to include a description indicating what environment the zone is for. The zone name is the same for each zone (for example, `testing.com`). 
     A single {{site.data.keyword.dns_short}} instance can only contain 10 zones.
     {: note}
  3. Add a zone to the instance of {{site.data.keyword.dns_short}}.
  4. In each respective zone, add specific VPCs as permitted networks. For example, for a development VPC, create a permitted network with the development VPC ID in the DNS zone for the development environment.
     While duplicate zone names are allowed in an account, duplicate zones cannot be associated with a single network.
     {: note}
  5. The result is that traffic from the development VPC only sees records from the development DNS zone and similarly for all the other environments. This way, you can use the same zone name in all environments, with the results tailored to each respective environment.

## Using {{site.data.keyword.dns_short}} with Split Horizon Capabilities
{: #using-dns-services-with-split-horizon-capabilities}

You can use {{site.data.keyword.dns_short}} to resolve `www.example.com` to a public address or to an internal network address. When the {{site.data.keyword.dns_short}} resolver receives a request, it checks whether the request is for a hostname defined within a private zone for the network where the request originated. If so, the hostname is resolved privately. Otherwise, the request is forwarded to a public resolver and the response returned to the requester. This allows for a hostname such as `www.example.com` to resolve differently on the internet versus on {{site.data.keyword.cloud_notm}}.

![Split Horizons](images/dns-svcs-overview.png "Split horizons image"){: caption="Figure 1. DNS workflow" caption-side="bottom"}
