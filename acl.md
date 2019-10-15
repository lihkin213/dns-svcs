---

copyright:
  years: 2019 
lastupdated: "2019-10-15"

keywords: dns, dns-svcs, DNS Services, Private DNS, dns vpc, Access Control Lists, permitted networks

subcollection: dns-svcs

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:DomainName: data-hd-keyref="DomainName"}
{:note: .note}
{:tip: .tip}
{:important: .important}
{:deprecated: .deprecated}
{:generic: data-hd-programlang="generic"}



# Managing permitted networks
{: #manage-acls}

{{site.data.keyword.cloud}} DNS Services is in Experimental Release. At this time the service is available to whitelisted customers only.
{: important}

You can control which VPC is permitted to perform name resolution for a DNS zone, by adding the VPC as a permitted network to the DNS Zone. The permitted network is used for Access Control mechanism.


## Create a permitted network
{: #create-acl-entry}

A DNS zone's initial state is `PENDING_NETWORK_ADD`, because its permitted network list is empty when the DNS zone is created. When a permitted network is added to the DNS zone's permitted networks, the state moves to `ACTIVE`.


**Request**

```json
curl -X POST \
         https://api.dns-svcs.test.cloud.ibm.com/v1/instances/$INSTANCE_ID/dnszones/$DNSZONE_ID/acls \
         -H "Authorization: $TOKEN" \
         -d '{
             "type": "vpc",
                 "acl_data":{
                     "vpc_crn":"crn:v1:staging:public:is:us-east:a/0821fa9f9ebcc7b7c9a0d6e9bf9442a4::vpc:b7246cdf-892a-4a6c-8fa9-491a5f585bd0"
                 }
         }'
```

**Parameters**

* DNSZONE_ID: When you create a zone, the DNSZONE_ID is returned in the response.

**Response**

```json
{
    "id": "b7246cdf-892a-4a6c-8fa9-491a5f585bd0",
        "created_on": "2019-09-11 13:46:51.68793557 +0000 UTC",
        "modified_on": "2019-09-11 13:46:51.68793557 +0000 UTC",
        "acl_data": {
            "vpc_crn": "crn:v1:staging:public:is:us-east:a/0821fa9f9ebcc7b7c9a0d6e9bf9442a4::vpc:b7246cdf-892a-4a6c-8fa9-491a5f585bd0"
        },
        "type": "vpc"
}
```

For future requests the ID in the response is referenced as `Permitted_Network_ID`.
{:note}

## Get a permitted network
{: #get-acl-entry}

List a particular permitted network from your instance using the Permitted Network ID.

**Request**

```json
curl -X GET \
         https://api.dns-svcs.test.cloud.ibm.com/v1/instances/$INSTANCE_ID/dnszones/$DNSZONE_ID/acls/$ACL_ID \
         -H "Authorization: $TOKEN"
```

**Response**

```json
{
    "id": "b7246cdf-892a-4a6c-8fa9-491a5f585bd0",
        "created_on": "2019-09-11 13:46:51.68793557 +0000 UTC",
        "modified_on": "2019-09-11 13:46:51.68793557 +0000 UTC",
        "acl_data": {
            "vpc_crn": "crn:v1:staging:public:is:us-east:a/0821fa9f9ebcc7b7c9a0d6e9bf9442a4::vpc:b7246cdf-892a-4a6c-8fa9-491a5f585bd0"
        },
        "type": "vpc"
}
```

## List permitted networks
{: #list-acls}

List all permitted network for your DNS zone.

**Request**

```json
curl -X GET \
         https://api.dns-svcs.test.cloud.ibm.com/v1/instances/$INSTANCE_ID/dnszones/$DNSZONE_ID/acls \
         -H "Authorization: $TOKEN"
```

**Response**

```json
{
    "acls": [
    {
        "id": "b7246cdf-892a-4a6c-8fa9-491a5f585bd0",
            "created_on": "2019-09-11 13:46:51.68793557 +0000 UTC",
            "modified_on": "2019-09-11 13:46:51.68793557 +0000 UTC",
            "acl_data": {
                "vpc_crn": "crn:v1:staging:public:is:us-east:a/0821fa9f9ebcc7b7c9a0d6e9bf9442a4::vpc:b7246cdf-892a-4a6c-8fa9-491a5f585bd0"
            },
            "type": "vpc"
    }
    ]
}
```

## Delete a permitted network
{: #delete-acl-entry}

Delete a particular permitted network from your instance. Unlink VPC from a zone.

**Request**

```json
curl -X DELETE \
         https://api.dns-svcs.test.cloud.ibm.com/v1/instances/$INSTANCE_ID/dnszones/$DNSZONE_ID/acls/$ACL_ID \
         -H "Authorization: $TOKEN"
```

**Response**
```
         HTTP 204 returned, no content in response
```
