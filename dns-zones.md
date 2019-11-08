---

copyright:
  years: 2019
lastupdated: "2019-10-30"

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
DNS zones can be managed through the {{site.data.keyword.cloud_full}} console, or the API. The following sections cover the console usage.

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

First store the API endpoint in a variable so you can use it in API requests without having to type the full URL. For example, to store the production endpoint in a variable, run this command:

```bash
dnssvcs_endpoint=https://api.dns-svcs.cloud.ibm.com
```
{:pre}

To verify that this variable was saved, run `echo $DNSSVCS_ENDPOINT` and make sure the response is not empty.

### Create a DNS zone
{: #create-dns-zone-api}

Create a new zone by using the following curl command:

**Request**

```bash
curl -X POST \
  $DNSSVCS_ENDPOINT/v1/instances/$INSTANCE_ID/dnszones \
  -H "Authorization: $TOKEN" \
  -d '{
	"name": "example.com",
	"description": "Example zone"
}'
```
{:pre}

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
{:pre}

For future reference, the "id" in response is used as `DNSZONE_ID`. 
{:note}

### Get a DNS Zone
{: #get-dns-zone-api}

Use the following command to get a zone which has already been created. 

**Request**

```bash
curl -X GET \
  $DNSSVCS_ENDPOINT/v1/instances/$INSTANCE_ID/dnszones/$DNSZONE_ID \
  -H "Authorization: $TOKEN"
```
{:pre}

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
{:pre}

### Update a DNS zone
{: #update-dns-zone-api}

Use the following command to update a zone which has already been created. The description and label are the only fields that can be updated. All other fields are read-only.

**Request**

```bash
curl -X PATCH \
  $DNSSVCS_ENDPOINT/v1/instances/$INSTANCE_ID/dnszones/$DNSZONE_ID \
  -H 'Content-Type: application/json' \
  -H "Authorization: $TOKEN" \
  -d '{
	  "description": "The DNS zone is used for VPCs in us-east region",
	  "label": "us-east"
}'

```
{:pre}

**Response**

```json
{
  "created_on": "2019-01-01T05:20:00.12345Z",
  "description": "The DNS zone is used for VPCs in us-east region",
  "id": "example.com:2d0f862b-67cc-41f3-b6a2-59860d0aa90e",
  "instance_id": "1407a753-a93f-4bb0-9784-bcfc269ee1b3",
  "label": "us-east",
  "modified_on": "2019-01-01T05:20:00.12345Z",
  "name": "example.com",
  "state": "PENDING_NETWORK_ADD"
}
```
{:pre}


### List DNS Zones
{: #list-dns-zones-api}

If you have a one or more zones in your domain you can list them by using the following curl command: 

**Request**

```bash
curl -X GET \
  $DNSSVCS_ENDPOINT/v1/instances/$INSTANCE_ID/dnszones \
  -H "Authorization: $TOKEN"
```
{:pre}

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
{:pre}

### Delete a DNS Zone
{: #delete-dns-zone-api}

**Request**

```bash
curl -X DELETE \
  $DNSSVCS_ENDPOINT/v1/instances/$INSTANCE_ID/dnszones/$DNSZONE_ID \
  -H "Authorization: $TOKEN"
```
{:pre}

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
{:pre}
