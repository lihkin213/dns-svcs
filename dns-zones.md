---

copyright:
  years: 2019
lastupdated: "2019-10-16"

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


# Managing DNS zones
{:#managing-dns-zones}

{{site.data.keyword.cloud}} DNS Services is in Experimental Release. At this time the service is available to whitelisted customers only.
{: important}

If you have not already created a DNS service instance, refer to [Create a DNS Services Instance](/docs/infrastructure/dns-svcs?topic=dns-svcs-getting-started#step-1-create-dns-services-instance) before managing DNS zones.

## Using the IBM Cloud console
{: #managing-dns-zones-ui}

### Creating DNS zone
{:#create-dns-zone-ui}

  1. From the resource page, select the desired DNS Services instance.
  2. Click the **Create Zone** button on the **DNS Zones** page. A panel appears.
  3. In the side panel, enter your zone name in the **Name** field.
  4. The **Label** and **Description** are optional fields.
  5. Click **Create Zone** button.

If the zone creation is successful, you are directed to the **Zone Details** page.

If the zone creation is unsuccessful, an error notification appears with information about what caused the error.

### Editing DNS zone
{:#edit-dns-zone-ui}

  1. From the **DNS Zones** page, select the desired zone. **Label** and **Description** options appear.
  2. To edit label, click on the edit icon for **Label**, enter the label and click **Save**.
  3. To edit description, click on the edit icon for **Description**, enter the description and click **Save**.

### Deleting DNS zone
{:#delete-dns-zone-ui}

  1. From the **DNS Zones** page, click the delete icon from the row for the zone you wish to delete. A confirmation dialog appears.
  2. Click **Delete** button.

## Using the API
{: #managing-dns-zones-api}

### Create a DNS zone
{: #create-dns-zone-api}

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

### Get a DNS Zone
{: #get-dns-zone-api}

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
### Update a DNS zone
{: #update-dns-zone-api}



### List DNS Zones
{: #list-dns-zones-api}

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

### Delete a DNS Zone
{: #delete-dns-zone-api}

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
