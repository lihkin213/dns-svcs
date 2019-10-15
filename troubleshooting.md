---

copyright:
  years: 2019
lastupdated: "2019-09-06"

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

## Unable to add permitted network
Check if you are trying to add duplicate zone and networks.

For example:
```
- Create zone1.com with network-1
  - Create zone1.com is successful
  - Add network-1 is successful

- Create duplicate zone1.com with network-1
  - Create zone1.com is successful
  - Add network-1 fails
```

Duplicate zone and networks cannot be added.
