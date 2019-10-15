---

copyright:
  years: 2019
lastupdated: "2019-10-15"

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


# Managing DNS records
{:#managing-dns-records}

{{site.data.keyword.cloud}} DNS Services is in Experimental Release. At this time the service is available to whitelisted customers only.
{: important}

## Adding DNS records
{:#adding-dns-records}

  1. From the DNS zones table click on the zone name to which you would like to add record(s). You will see more details on selected zone. 
  2. Click on `Add Record` button. You will see a side panel for creating a record.

You can use the **Type** dropdown to select the type of record you want to create. Each DNS record type has a Name and Time-To-Live (TTL) associated with it. 

Whatever is entered into the Name field will have domain name appended to it unless domain name is manually appended in the field already (for example if `www` or `www.example.com` is typed into the field, the API will handle both as `www.example.com`). If the exact domain name is typed into the name field, then it won't be appended on itself (for example, `example.com` will be handled as `example.com`). However, the list of DNS records will only show the names without the domain name being tacked on, so `www.example.com` is shown as `www` and `example.com` will be shown as `example.com`. The TTL will have a default value of `1 min`, but can be changed by the user.

### A Type record

To add this record type, valid values must exist in the **Name** and **IPv4 Address** fields. A **TTL** also can be specified from the dropdown menu, with a default value of `1 min`.

    Required Fields: Name, IPv4 Address
    Optional Field: TTL (Default value is 1 min)

### AAAA Type record

To add this record type, valid values must exist in the **Name** and **IPv6 Address** fields. A **TTL** also can be specified from the dropdown menu, with the default value of `1 min`.

    Required Fields: Name, IPv6 Address
    Optional Field: TTL (Default value is 1 min)

### CNAME Type record

To add this record type, a valid value must exist in the **Name** field and a fully qualified domain name must be in the **Target** (FQDN) field. A **TTL** also can be specified from the dropdown menu, with the default value of `1 min`.

    Required Fields: Name, Target (for CNAME)
    Optional Field: TTL (Default value is 1 min)

### MX Type record

To add this record type, a valid value must exist in the **Name** field, a fully qualified domain name must be in the **Mail Server** (FQDN)field and a valid number must exist in the **Priority** field. A **TTL** also can be specified from the dropdown menu, with the default value of `1 min`.

    Required Fields: Name, Mail Server
    Optional Fields: TTL (Default value is 1 min), Priority (Default value is 1)

### PTR Type record

To add this record type, an existing A or AAAA records must be created beforehand that are not already associated with another PTR record. A filterable dropdown will allow user to select an existing record. Selecting an existing record is mandatory. A **TTL** also can be specified from the dropdown menu, with the default value of `1 min`.

    Required Fields: Select existing record
    Optional Fields: TTL (Default value is 1 min)

### SRV Type record

To add this record type, valid values must exist in the **Name**, **Service Name** and **Target** fields. Use the dropdown menu to select a **protocol**, which defaults to the UDP protocol. Additionally, you can specify **Priority**, **Weight** and **Port**. These three fields default to a value of 1. A **TTL** also can be specified from the dropdown menu, with the default value of `1 min`.

    Required Fields: Name, Service Name, Target
    Optional Fields: TTL (Default value is Automatic), Protocol (Default value is UDP),
                     Priority (Default value is 1), Weight (Default value is 1), Port (Default value is 1)

### TXT Type record

To add this record type, valid values must exist in the **Name** and **Content** fields. A **TTL** also can be specified from the dropdown menu, with the default value of `1 min`.

    Required Fields: Name, Content
    Optional Field: TTL (Default value is 1 min)

## Updating DNS records
{:#updating-dns-records}

In each record row, you can click the **Edit** icon, which will open a side panel, which you can use to update the record.

## Deleting DNS records
{:#deleting-dns-records}

In each record row, you can click the **Delete** icon, which opens a dialog box to confirm the delete process.
