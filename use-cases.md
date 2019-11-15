---

copyright:
  years: 2019
lastupdated: "2019-10-08"

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

{{site.data.keyword.cloud}} DNS Services is in Experimental Release. At this time the service is available to whitelisted customers only.
{: important}

This section covers some possible use cases you may have while using DNS Services.
{:shortdesc}

## Using DNS Services for VPC
{: #using-dns-services-for-vpc}

  1. Create a VPC instance.
  2. Create a DNS Services instance.
  3. Add a DNS zone to the DNS Services instance.
  4. Designate the VPC instance as a permitted network for the DNS zone.
  5. Add a DNS Resource record to the DNS zone.
  6. Configure VPC servers to use DNS Services resolvers.
  7. Verify name resolution of the DNS Resource record works from within the VPC.


## Creating multiple zones with duplicate names
{: #creating-multiple-zones-with-duplicate-names}

  1. Create an instance of DNS Services
  2. Create a DNS zone for each environment (for example, production, staging, development, testing)    
      * When creating the zone, be sure to include a description indicating what environment the zone is for.
      * The zone name will be the same for each zone (for example, `testing.com`)
      * Keep in mind that a single DNS service instance can only contain 10 zones.    
  3. Add a zone to the instance of DNS Services
  4. In each respective zone, add specific VPCs as permitted networks
      * For example, for a dev VPC, create a permitted network with the dev VPC ID in the DNS zone for the dev environment.
      * Note that while duplicate zone names are allowed in an account, duplicate zones cannot be associated with a single network.
  5. The result is that traffic from the dev VPC will only see records from the dev DNS zone and similarly for all the other environments. This way, the same zone name can be used in all environments but the results will be tailored to each respective environment.

## Using DNS Services with Split Horizon Capabilities
{: #using-dns-services-with-split-horizon-capabilities}

You can use DNS Services to resolve `www.test.com` to a public address or an internal network's address. When the DNS Services resolver receives a request, it checks whether the request is for a hostname defined within a private zone for the network where the request originated. If so, the hostname is resolved privately. Otherwise, the request is forwarded to a public resolver and the response returned to the requester. This allows for a hostname such as `www.test.com` resolve differently on the Internet versus on IBM Cloud.

![Split Horizons](images/split-horizon.png "Split horizons image"){: caption="Figure 1. DNS workflow" caption-side="bottom"}
