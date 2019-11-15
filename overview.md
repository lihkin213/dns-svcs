---

copyright:
  years: 2019
lastupdated: "2019-10-09"

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

# About DNS Services
{: #about-dns-services}

{{site.data.keyword.cloud}} DNS Services is in Experimental Release. At this time the service is available to whitelisted customers only.
{: important}

To better understand IBM Cloud DNS Services, it helps to know more about DNS in general.
{:shortdesc}

## DNS overview
{: #dns-overview}

Computers on a network can find one another by IP addresses. To make it easier to work within a computer network such as the internet, people can use a Domain Name System (DNS) to associate human-friendly domain names with these addresses, similar to a phonebook. A DNS can also associate other information beyond just computer network addresses to domain names.

That way, people can use human friendly domain names instead of obscure, hard-to-remember, machine-oriented data.

## DNS Services
{: dns-services-overview}

IBM Cloud DNS Services allow you to:
* Create DNS zones that are collections for holding domain names
* Create DNS resource records under these zones
* Specify access controls used for the DNS resolution of resource records on a zone-wide level

IBM Cloud DNS Services also maintains its own world-wide set of DNS resolvers. Computer machines provisioned under {{site.data.keyword.cloud_notm}} on an {{site.data.keyword.cloud_notm}} network can use resource records configured through IBM Cloud DNS Services by querying IBM Cloud DNS Services' resolvers.

Resource records and zones configured through IBM Cloud DNS Services:
* Are separated from the wider, public DNS and their publicly accessible records
* Are hidden from machines outside of and not part of the {{site.data.keyword.cloud_notm}} network
* Are accessible only from machines that you authorize on the {{site.data.keyword.cloud_notm}} network
* Are resolvable only via the resolvers provided by the service


![Diagram of DNS services overview](images/dns-svcs-overview.png "Diagram of DNS services overview"){: caption="Figure 1. A diagram of DNS Services workflow" caption-side="bottom"}


Those who need privacy can use IBM Cloud DNS Services to ensure a level of privacy for information specified in their zones and resource records.

While the Cloud DNS Service is accessible globally on the IBM Cloud network, the us-south and eu-de MZRs are optimized for latency at this time. Other MZRs will be optimized over time.

For provisioning and configuring DNS records for public DNS resolution, refer to [{{site.data.keyword.cis_full_notm}}](/docs/infrastructure/cis?topic=cis-about-ibm-cloud-internet-services-cis) ({{site.data.keyword.cis_short_notm}}).
