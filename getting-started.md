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

# Getting started with IBM Cloud DNS Services
{: #getting-started}

{{site.data.keyword.cloud}} DNS Services is in Experimental Release. At this time the service is available to whitelisted customers only.
{: important}

IBM Cloud DNS Services provides private DNS to Virtual Private Cloud (VPC) users. Private DNS zones are resolvable only on IBM Cloud, and only from explicitly permitted networks such as VPCs in an account.

This is the process to get started:

- Create a DNS Services Instance
- Add a DNS Zone
- Add VPC as a Permitted Network to the DNS Zone
- Add DNS Resource Records to the DNS Zone
- Ensure that servers in the VPC use the Private DNS resolvers
- Test if the DNS name resolution works from the VPC

These steps enable you to query any record added underneath the zone from the Permitted VPC Network.

## Before you begin

To use DNS Services you must have a VPC created in the IBM Cloud. Follow this link to [Create the VPC](/docs/vpc-on-classic?topic=vpc-on-classic-creating-a-vpc-using-the-ibm-cloud-console).

The VPC must be configured to use the Private DNS resolvers (161.26.0.7, 161.26.0.8). For example, on some Linux distributions, this can be done by editing the file `/etc/resolv.conf`. It may also be possible to override the default DNS resolvers via cloud init during server boot up. Consult your operating system manuals for more information. When editing configuration files, ensure that you keep a backup copy of the existing configuration in case it needs to be restored. An easier way to use private DNS resolvers will be introduced in the future.

Note that while the private DNS resolvers are required to resolve private DNS names, they also resolve public DNS names if the request is for a name that is not defined to be in a private DNS zone for the originating network/VPC.

## Step 1: Create a DNS Services Instance
{: #step-1-create-dns-services-instance}

Open the {{site.data.keyword.cloud_notm}} catalog page and select `Networking`. Click on the `DNS Services` tile to create a `DNS Services` instance. Currently the default and only available plan is free.

## Step 2: Add a DNS Zone

### Using the IBM Cloud Console
- From the resource page, select the desired DNS Services instance
- Click the "Create Zone" button on the DNS Zones page
- In the side panel, input your zone name
- The label and description are optional fields
- Click "Create Zone"
- If the zone creation is successful, you will be directed to the Zone Details page

For example, a zone name could be `example.com`. Note that only 2 level zones are supported as zone names (for example, `example.com` is permitted, but `subdomain.example.com` is not, although subdomains can be defined within the zone once created).

For steps on using the API, follow the steps in the detailed guide to [Creating a zone](/docs/dns-svcs?topic=dns-svcs-managing-dns-zones-api#managing-dns-zones-api).


## Step 3: Add VPC as a Permitted Network to the DNS Zone

### Using the IBM Cloud Console
- If you are not already on the Zone Details page, navigate there by selecting the desired zone from the table on the DNS Zones page
- Select the "Permitted Networks" tab
- Click the "Add Network" button
- In the side panel, select the region of your VPC from the "Network Region" dropdown
- Select the desired VPC from the "Network" dropdown that appears
- Click "Add Network"

This request adds the VPC network to the zone, thereby giving the network access to the zone.

For steps on using the API, follow the steps in the detailed guide to [Managing permitted networks](/docs/dns-svcs?topic=dns-svcs-managing-permitted-networks-api#managing-permitted-networks-api).


## Step 4: Add DNS Resource Records

### Using the IBM Cloud Console
- If you are not already on the Zone Details page, navigate there by selecting the desired zone from the table on the DNS Zones page
- Select the "DNS Records" tab
- Click the "Add Record" button
- In the side panel, select the type of DNS record you would like to add from the "Type" dropdown
- Input the required data for the type of DNS record you selected
- Click "Add Record"

For steps on using the API, follow the steps in the detailed guide to [Managing DNS records](/docs/dns-svcs?topic=dns-svcs-managing-dns-records-api#managing-dns-records-api).

## Step 5: Test if the DNS Name resolution works from the VPC

Test whether the zone resolution works using a dig from the VPC. The following command should yield a resolution as the result.

```shell
dig www.example.com
```
