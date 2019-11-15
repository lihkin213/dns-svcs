---

copyright:
  years: 2019
lastupdated: "2019-10-29"

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

# Troubleshooting DNS Services
{: #troubleshooting-dns-services}

{{site.data.keyword.cloud}} DNS Services is in Experimental Release. At this time the service is available to whitelisted customers only.
{: important}

This section gives troubleshooting tips for your DNS Services.
{:shortdesc}

## Unable to perform name resolution with NXDOMAIN error.
{:#unable-to-perform-name-resolution-with-nxdomain-error}
  * Verify the server you are sending the request from is configured to use the DNS resolvers `161.26.0.7` or `161.26.0.8`
  * Verify the server you are sending the request from is part of a VPC that has been added as a permitted network to the DNS zone.
  * Verify the FQDN for which name resolution is attempted has a Resource Record in the DNS zone.
  * Verify the DNS request is using the correct Resource record type in the query.

## Adding Permitted Network gave an error that VPC does not have Cloud Service Endpoint (CSE) enabled.
{:#adding-permitted-network-cse-not-enabled}
  * By default only VPCs created on or after 10/09/2019 are enabled to use with Private DNS.
  * For to VPCs created before that, as a permitted network, please review https://www.ibm.com/support/pages/node/1086243 to contact support and get the VPC CSE enabled.
  * You will then be able to add this VPC for your DNS zone.

## Unable to add permitted network
{:#unable-to-add-permitted-network}
Check if you are trying to add duplicate zone and networks.

For example:

- Create zone1.com with network-1
  - Create zone1.com is successful
  - Add network-1 is successful

- Create duplicate zone1.com with network-1
  - Create zone1.com is successful
  - Add network-1 fails


Duplicate zone and networks cannot be added.
