---

copyright:
  years: 2019  
lastupdated: "2019-10-14"

keywords: dns, dns-svcs, DNS Services, Private DNS, dns vpc

subcollection: dns-svcs

---

# Setting up your DNS instance
{: #setting-up-your-dns-instance}

{{site.data.keyword.cloud}} DNS Services is in Experimental Release. At this time the service is available to whitelisted customers only.
{: important}

This section describes how to set up a DNS instance, DNS zones, permitted networks, and resource records.

## Creating a DNS instance
{: #creating-a-dns-instance}

If your account is enabled for the experimental DNS Services, it appears in the experimental catalog at https://test.cloud.ibm.com/catalog/labs. You can also navigate directly to the DNS Services instance creation by going to https://test.cloud.ibm.com/catalog/services/dns-services.

## Creating a DNS zone
{: #creating-a-dns-zone}

### Before you begin
{: #dns-zone-before-you-begin}
You must create a VPC so that you can link your DNS zone to the VPC.

After you gather details about your instance, you can create a new DNS zone by using the following curl command:

**Request**
```json
curl -X POST \
  https://api.dns-svcs.test.cloud.ibm.com/v1/instances/$INSTANCE_ID/dnszones \
  -H "Authorization: $TOKEN" \
  -d '{
        "name": "example.com",
        "description": "The DNS zone is used for VPCs in us-east region",
        "label": "us-east"
  }'
```

* INSTANCE_ID: GUID of the instance
* TOKEN: IAM OAUTH token

**Response**
```json
{
  "id": "example.com:2d0f862b-67cc-41f3-b6a2-59860d0aa90e",
  "created_on": "2019-01-01T05:20:00.12345Z",
  "modified_on": "2019-01-01T05:20:00.12345Z",
  "instance_id": "1407a753-a93f-4bb0-9784-bcfc269ee1b3",
  "name": "example.com",
  "description": "The DNS zone is used for VPCs in us-east region",
  "state": "pending_network_add",
  "label": "us-east"
}
```


## Creating a permitted network
{: #creating-an-acl}

Private DNS allows name resolution only from a VPC that has been added to the DNS Zone. 

When a DNS zone first gets created, its Status is `PENDING_NETWORK_ADD`. In order to move the zone to an `ACTIVE` state, add an entry for your VPC to the zone's permitted network.

By adding your VPC to your zone's permitted network, compute instances on your VPC will have access to these resource records.

**Request**
```json
curl -X POST \
  https://api.dns-svcs.test.cloud.ibm.com/v1/instances/$INSTANCE_ID/dnszones/$DNSZONE_ID/acls \
  -H "Authorization: $TOKEN" \
  -d '{
        "type": "vpc",
        "acl_data": {
            "vpc_crn": "crn:v1:staging:public:is:us-east:a/40705ee14536813e2385f26c20be24a5::vpc:ed5e3cdd-8a4f-45ce-bae4-2774cb028caf"
        }
  }'
```

**Response**
```json
{
  "id": "fecd0173-3919-456b-b202-3029dfa1b0f7",
  "created_on": "2019-01-01T05:20:00.12345Z",
  "modified_on": "2019-01-01T05:20:00.12345Z",
  "acl_data": {
    "vpc_crn": "crn:v1:staging:public:is:us-east:a/40705ee14536813e2385f26c20be24a5::vpc:ed5e3cdd-8a4f-45ce-bae4-2774cb028caf"
  },
  "type": "vpc"
}
```

### Creating an "A" resource record
{: #creating-a-resource-records}

An A Record (Address Record) is a DNS resource record that associates a domain or subdomain to an IPv4 address.

**Request**
```json
curl -X POST \
  https://api.dns-svcs.test.cloud.ibm.com/v1/instances/$INSTANCE_ID/dnszones/$DNSZONE_ID/resource_records \
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

* `name`: FQDN (such as www.example.com) or the host (such as www)
* `type`: Type of Record - A, AAAA, SRV, etc.
* `ip`: IP address for the Name.
* `ttl`: Time to live for the RR

**Response**

```json
{
   "created_on":"2019-09-13 19:56:42.484382585 +0000 UTC",
   "modified_on":"2019-09-13 19:56:42.484382585 +0000 UTC",
   "rtype":"A",
   "ttl":300,
   "name":"www.example.com.testZone.com",
   "id":"A:786c07c7-173e-473b-aa09-c186601a5709",
   "rdata":{
      "ip":"1.2.6.7"
   }
}
```

## Verifying the setup
{: #verifying-the-setup}

Verify that your instance, zone and record are performing correctly by executing the following dig command:

```dig @161.26.0.7 <Record type> <record name>```

Example :

```dig @161.26.0.7 A xyz.example.com```
