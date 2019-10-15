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

# Managing DNS zones
{: #Manage-dns-zones}

{{site.data.keyword.cloud}} DNS Services is in Experimental Release. At this time the service is available to whitelisted customers only.
{: important}

## Before you begin
{: #before-you-begin-configuring-zones}

Create an instance of DNS Services.

After you create your own instance, create a zone to host in that instance. The zone must be two levels deep. Note that this doesn't limit the depth of hostnames within the zone. For example, within the zone `example.com`, you can add A records for `hostname.example.com`, or `hostname.subdomain.example.com`. 

Unlike public DNS domains, private domains are not registered with a registrar. They exist solely within IBM Cloud DNS Services. To enable split horizon DNS operation, we allow arbitrary domain names with a few restrictions. This can result in a private DNS domain with the same name as a public DNS domain. When such a private domain is attached to a network such as a VPC, the private domain will have higher precedence in that network.

### Create a DNS zone
{: #create-a-dns-zone}

Create a new zone by using the following curl command:

**Request**

```json
curl -X POST \
  https://api.dns-svcs.test.cloud.ibm.com/v1/$CRN/zones \
  -H "X-Auth-User-Token: $TOKEN" \
  -d '{
	"name": "example.com",
	"description": "Example zone"
}'
```

**Response**

```json
{
    "success": true,
    "result": {
        "id": "ed10e4b2-8a64-4afa-a4e2-9e60a766d079",
        "created_on": "2019-07-24 12:30:58.357201205 +0000 UTC",
        "modified_on": "2019-07-24 12:30:58.357201205 +0000 UTC",
        "instance_id": "1a34bda8-9c94-4232-bea7-7df163b21d23",
        "name": "example.com",
        "description": "Example zone",
        "state": "PENDING_NETWORK_ADD",
        "tag": "example.com:ed10e4b2-8a64-4afa-a4e2-9e60a766d079"
    },
    "errors": [],
    "messages": []
}
```

For future reference, the "tag" in response is used as `ZONE_TAG`. 
{:note}

## Get a DNS Zone
{: #get-a-dns-zone}

Use the following command to get a zone which has already been created. 

**Request**

```json
curl -X GET \
  https://api.dns-svcs.test.cloud.ibm.com/v1/$CRN/zones/$ZONE_TAG \
  -H "X-Auth-User-Token: $TOKEN"
```

**Response**

```json
{
    "success": true,
    "result": {
        "id": "ed10e4b2-8a64-4afa-a4e2-9e60a766d079",
        "created_on": "2019-07-24 12:30:58.357201205 +0000 UTC",
        "modified_on": "2019-07-24 12:30:58.357201205 +0000 UTC",
        "instance_id": "1a34bda8-9c94-4232-bea7-7df163b21d23",
        "name": "example.com",
        "description": "Example zone",
        "state": "PENDING_NETWORK_ADD",
        "tag": "example.com:ed10e4b2-8a64-4afa-a4e2-9e60a766d079"
    },
    "errors": [],
    "messages": []
}
```
## Update a DNS zone
{: #update-a-dns-zone}



## List DNS Zones
{: #list-dns-zones}

If you have a one or more zones in your domain you can list them by using the following curl command: 

**Request**

```json
curl -X GET \
  https://api.dns-svcs.test.cloud.ibm.com/v1/$CRN/zones \
  -H "X-Auth-User-Token: $TOKEN"
```

**Response**

```json
{
    "success": true,
    "result": [
        {
            "id": "ed10e4b2-8a64-4afa-a4e2-9e60a766d079",
            "created_on": "2019-07-24 12:30:58.357201205 +0000 UTC",
            "modified_on": "2019-07-24 12:30:58.357201205 +0000 UTC",
            "instance_id": "1a34bda8-9c94-4232-bea7-7df163b21d23",
            "name": "example.com",
            "description": "Example zone",
            "state": "PENDING_NETWORK_ADD",
            "tag": "example.com:ed10e4b2-8a64-4afa-a4e2-9e60a766d079"
        }
    ],
    "errors": [],
    "messages": []
}
```

## Delete a DNS Zone
{: #delete-a-dns-zone}

**Request**

```json
curl -X DELETE \
  https://api.dns-svcs.test.cloud.ibm.com/v1/$CRN/zones/$ZONE_TAG \
  -H "X-Auth-User-Token: $TOKEN"
```

**Response**

```json
{
    "success": true,
    "result": {
        "id": "ed10e4b2-8a64-4afa-a4e2-9e60a766d079"
    },
    "errors": [],
    "messages": []
}
```
