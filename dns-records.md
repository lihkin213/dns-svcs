---

copyright:
  years: 2019
lastupdated: "2019-11-04"

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

## Using the IBM Cloud console
{: #managing-dns-records-ui}
DNS records can be managed from the {{site.data.keyword.ccloud_full}} console, or the API. The following sections cover the console usage.
{:shortdesc}

### Adding DNS records
{:#adding-dns-records}

  1. From the DNS zones table, click on the zone name to which you want to add record(s). You will see more details on the selected zone.
  2. Click the **Add Record** button to display a panel for creating a record.

You can use the **Type** dropdown to select the type of record you want to create. Each DNS record type has a Name and Time-To-Live (TTL) associated with it.

Whatever you enter into the Name field has domain name appended to it unless domain name is manually appended in the field already (for example if **`www`** or **`www.example.com`** is typed into the field, the API will handle both as **`www.example.com`**). If the exact domain name is typed into the name field, then it won't be appended on itself (for example, **`example.com`** will be handled as **`example.com`**). However, the list of DNS records only show the names without the domain name added on. As a result, **`www.example.com`** displays as **`www`** and **`example.com`** as **`example.com`**.

The TTL has a default value of **`1 min`**, but can be changed by the user.
{:note}

#### A Type record
{:#a-record}

To add this record type, valid values must exist in the **Name** and **IPv4 Address** fields. A **TTL** can also be specified from the dropdown menu, with a default value of **`1 min`**.

Required Fields:
* Name
* IPv4 Address
* TTL (Default value is 1 min)

#### AAAA Type record
{:#aaaa-record}

To add this record type, valid values must exist in the **Name** and **IPv6 Address** fields. A **TTL** can also be specified from the dropdown menu, with the default value of **`1 min`**.

Required Fields:
* Name
* IPv6 Address
* TTL (Default value is 1 min)

#### CNAME Type record
{:#cname-record}

To add this record type, a valid value must exist in the **Name** field and a fully qualified domain name must be in the **Target** (FQDN) field. A **TTL** can also be specified from the dropdown menu, with the default value of **`1 min`**.

Required Fields:
* Name
* Target (for CNAME)
* TTL (Default value is 1 min)

#### MX Type record
{:#mx-record}

To add this record type, a valid value must exist in the **Name** field, a fully qualified domain name must be in the **Mail Server** (FQDN)field, and a valid number must exist in the **Priority** field. A **TTL** can also be specified from the dropdown menu, with the default value of **`1 min`**.

Required Fields:
* Name
* Mail Server
* TTL (Default value is 1 min)
* Priority (Default value is 1)

#### PTR Type record
{:#ptr-record}

To add this record type, an existing A or AAAA records must be created beforehand that are not already associated with another PTR record. A dropdown allows you to select an existing record, and doing so is mandatory. A **TTL** can also be specified from the dropdown menu, with the default value of **`1 min`**.

Required Fields:
* Select existing record
* TTL (Default value is 1 min)

#### SRV Type record
{:#srv-record}

To add this record type, valid values must exist in the **Name**, **Service Name** and **Target** fields. Use the dropdown menu to select a **protocol**, which defaults to the UDP protocol. Additionally, you can specify **Priority**, **Weight** and **Port**. These three fields default to a value of **`1`**. A **TTL** can also be specified from the dropdown menu, with the default value of **`1 min`**.

Required Fields:
* Name
* Service Name
* Target
* TTL (Default value is 1 min)
* Protocol (Default value is UDP)
* Priority (Default value is 1)
* Weight (Default value is 1)
* Port (Default value is 1)

#### TXT Type record
{:#txt-record}

To add this record type, valid values must exist in the **Name** and **Content** fields. A **TTL** can also be specified from the dropdown menu, with the default value of **`1 min`**.

Required Fields:
* Name
* Content
* TTL (Default value is 1 min)

### Updating DNS records
{:#updating-dns-records}

In each record row, click the **Edit** icon to open a panel where you can update the record.

### Deleting DNS records
{:#deleting-dns-records}

In each record row, click the **Delete** icon to open a panel where you can confirm the delete process.

## Using the API
{: #managing-dns-records-api}

First store the API endpoint in a variable so you can use it in API requests without having to type the full URL. For example, to store the production endpoint in a variable, run this command:

```bash
dnssvcs_endpoint=https://api.dns-svcs.cloud.ibm.com
```
{:pre}

To verify that this variable was saved, run **`echo $DNSSVCS_ENDPOINT`** and make sure the response is not empty.

### Create resource record of type 'A'
{: #create-resource-record-api}

**Request**

```bash
curl -X POST \
  $DNSSVCS_ENDPOINT/v1/instances/$INSTANCE_ID/dnszones/$DNSZONE_ID/resource_records \
  -H "Authorization: $TOKEN" \
  -d '{
	"name":"www.example.com",
	"type":"A",
	"rdata": {
            "ip":"1.2.6.7"
        },
 	"ttl":300
}'
```
{:pre}

**Response**

```json
{    
    "id": "fa57d5d0-7729-4770-af27-6d7f8dce860c",
    "created_on": "2019-08-12 08:03:03.910471016 +0000 UTC",
    "modified_on": "2019-08-12 08:03:03.910471016 +0000 UTC",
    "rtype": "A",
    "ttl": 300,
    "name": "www.example.com",
    "id": "A:fa57d5d0-7729-4770-af27-6d7f8dce860c",
    "rdata": {
        "ip": "1.2.6.7"
    }
}
```
{:pre}

### Create resource record of type 'SRV'
{: #create-srv-resource-record-api}

**Request**

```bash
curl -X POST \
  $DNSSVCS_ENDPOINT/v1/instances/$INSTANCE_ID/dnszones/$DNSZONE_ID/resource_records \
  -H "Authorization: $TOKEN" \
  -d '{
	"type": "SRV",
	"name": "example.com",
	"service": "srv",
	"protocol": "udp",
	"rdata": {
		"priority": 100,
		"weight": 100,
		"port": 8000,
		"target": "siphost.com"
	}
}'
```
{:pre}

**Response**

```json
{    
    "created_on": "2019-08-16 08:07:41.113606 +0000 UTC",
    "modified_on": "2019-08-16 08:07:41.113606 +0000 UTC",
    "rtype": "SRV",
    "ttl": 60,
    "name": "example.com",
    "id": "SRV:7562b1f9-1a6a-4189-b794-dd84c91d6a28",
    "rdata": {
        "priority": 100,
        "weight": 100,
        "port": 8000,
        "target": "siphost.com"
    },
    "service": "srv",
    "protocol": "udp"
}
```
{:pre}

### Create resource record of type 'TXT'
{: #create-txt-resource-record-api}

**Request**

```bash
curl -X POST \
  $DNSSVCS_ENDPOINT/v1/instances/$INSTANCE_ID/dnszones/$DNSZONE_ID/resource_records \
  -H "Authorization: $TOKEN" \
  -d '{
	"type": "TXT",
	"name": "txt.example.com",
	"rdata": {
		"txtdata": "txt strings"
	}
}'
```
{:pre}

**Response**

```json
{
    "created_on": "2019-08-16 08:15:53.360664 +0000 UTC",
    "modified_on": "2019-08-16 08:15:53.360664 +0000 UTC",
    "rtype": "TXT",
    "ttl": 60,
    "name": "txt.example.com",
    "id": "TXT:c6221d5f-69d7-4717-9951-4f69b2680fd4",
    "rdata": {
        "txtdata": "txt strings"
    }
}
```
{:pre}

### Create resource record of type 'MX'
{: #create-amx-resource-record-api}

**Request**

```bash
curl -X POST \
  $DNSSVCS_ENDPOINT/v1/instances/$INSTANCE_ID/dnszones/$DNSZONE_ID/resource_records \
  -H "Authorization: $TOKEN" \
  -d '{
	"type": "MX",
	"name": "mx1.example.com",
	"rdata": {
		"exchange": "mailserver.example.com",
		"preference": 10
	}
}'
```
{:pre}

**Response**

```json
{
    "created_on": "2019-08-16 08:21:20.308716 +0000 UTC",
    "modified_on": "2019-08-16 08:21:20.308716 +0000 UTC",
    "rtype": "MX",
    "ttl": 60,
    "name": "mx1.example.com",
    "id": "MX:8e1b201e-00dd-46a0-a3ec-46573f908870",
    "rdata": {
        "preference": 10,
        "exchange": "mailserver.example.com"
    }
}
```
{:pre}

### Create resource record of type 'PTR'
{: #create-ptr-resource-record-api}

**Request**

```bash
curl -X POST \
  $DNSSVCS_ENDPOINT/v1/instances/$INSTANCE_ID/dnszones/$DNSZONE_ID/resource_records \
  -H "Authorization: $TOKEN" \
  -d '{
	"type": "PTR",
	"name": "192.168.10.100",
	"rdata": {
	   "ptrdname": "www1.example.com"
	}
}'
```
{:pre}

**Response**

```json
{
    "created_on": "2019-08-30 06:48:16.971764628 +0000 UTC",
    "modified_on": "2019-08-30 06:48:16.971764628 +0000 UTC",
    "rtype": "PTR",
    "ttl": 60,
    "name": "100.10.168.192.in-addr.arpa",
    "id": "PTR:a47dd63a-e65a-4280-8f53-3cdb433cc78a",
    "rdata": {
        "ptrdname": "www1.example.com"
    }
}
```
{:pre}

### Create resource record of type 'CNAME'
{: #create-cname-resource-record-api}

**Request**

```bash
curl -X POST \
  $DNSSVCS_ENDPOINT/v1/instances/$INSTANCE_ID/dnszones/$DNSZONE_ID/resource_records \
  -H "Authorization: $TOKEN" \
  -d '{
	"type": "CNAME",
	"name": "cname.example.com",
	"rdata": {
	   "cname": "clientinterface.com"
	}
}'
```
{:pre}

**Response**

```json
{
    "created_on": "2019-08-16 08:29:36.710416 +0000 UTC",
    "modified_on": "2019-08-16 08:29:36.710416 +0000 UTC",
    "rtype": "CNAME",
    "ttl": 60,
    "name": "cname.example.com",
    "id": "CNAME:c95916ba-5504-499a-943a-21f5befe92b5",
    "rdata": {
        "cname": "clientinterface.com"
    }
}
```
{:pre}


### Create resource record of type 'AAAA'
{: #create-aaaa-resource-record-api}

**Request**

```bash
curl -X POST \
  $DNSSVCS_ENDPOINT/v1/instances/$INSTANCE_ID/dnszones/$DNSZONE_ID/resource_records \
  -H "Authorization: $TOKEN" \
  -d '{
	"type": "AAAA",
	"name": "test.example.com",
	"rdata": {
	   "ip": "8000::2000"
	}
}'
```
{:pre}

**Response**

```json
{
    "created_on": "2019-08-16 08:34:38.311539 +0000 UTC",
    "modified_on": "2019-08-16 08:34:38.311539 +0000 UTC",
    "rtype": "AAAA",
    "ttl": 60,
    "name": "test.example.com",
    "id": "AAAA:894e165b-f066-434d-9b58-4afc2dca62c9",
    "rdata": {
        "ip": "8000::2000"
    }
}
```
{:pre}

### Get a resource record
{: #get-resource-record-api}

**Request**

```bash
curl -X GET \
  $DNSSVCS_ENDPOINT/v1/instances/$INSTANCE_ID/dnszones/$DNSZONE_ID/resource_records/$RECORD_ID \
  -H "Authorization: $TOKEN"
```
{:pre}

**Response**

```json
{
    "created_on": "2019-08-12 08:03:03.910471016 +0000 UTC",
    "modified_on": "2019-08-12 08:03:32.875065176 +0000 UTC",
    "rtype": "A",
    "ttl": 300,
    "name": "www.example.com",
    "id": "A:fa57d5d0-7729-4770-af27-6d7f8dce860c",
    "rdata": {
        "ip": "9.4.6.7"
    }
}
```
{:pre}

### List resource records
{: #list-resource-records-api}

**Request**

```bash
curl -X GET \
  $DNSSVCS_ENDPOINT/v1/instances/$INSTANCE_ID/dnszones/$DNSZONE_ID/resource_records \
  -H "Authorization: $TOKEN"
```
{:pre}

**Response**

```json
{
    "resource_records": [
        {
            "created_on": "2019-08-30 04:10:25.092468565 +0000 UTC",
            "modified_on": "2019-08-30 04:10:25.092468565 +0000 UTC",
            "rtype": "A",
            "ttl": 60,
            "name": "www.example.com",
            "id": "A:ec0c4ee2-5d1f-4066-bcf2-dc9f3122c639",
            "rdata": {
                "ip": "192.168.10.100"
            }
        }
    ]
}
```
{:pre}

### Update a resource record
{: #update-resource-record-api}

**Request**

```bash
curl -X PUT \
  $DNSSVCS_ENDPOINT/v1/instances/$INSTANCE_ID/dnszones/$DNSZONE_ID/resource_records/$RECORD_TAG \
  -H "Authorization: $TOKEN" \
  -d '{
	"name":"www",
	"rdata": {
            "ip":"7.7.7.7"
        },
 	"ttl":300
}'
```
{:pre}

**Response**

```json
{
    "created_on":"2019-09-10 20:03:25.249355942 +0000 UTC",
    "modified_on":"2019-09-11 16:13:17.350043736 +0000 UTC",
    "rtype":"A",
    "ttl":300,
    "name":"www",
    "id":"A:139eb9f3-c646-4eb6-92fa-3ddabfb1b84f",
    "rdata":{
        "ip":"7.7.7.7"
    }
}
```
{:pre}

### Delete a resource record
{: #delete-resource-record-api}

**Request**

```bash
curl -X DELETE \
  $DNSSVCS_ENDPOINT/v1/instances/$INSTANCE_ID/dnszones/$DNSZONE_ID/resource_records \
  -H "Authorization: $TOKEN"
```
{:pre}

**Response**

```json
HTTP 204 is returned, no content in response.
```
{:pre}
