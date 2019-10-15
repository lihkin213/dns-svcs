---

copyright:
  years: 2019  
lastupdated: "2019-10-09"

keywords: dns-svcs, DNS Services, Private DNS

subcollection: dns-svcs


---

# Managing Resource records
{: #manage-resource-records}

{{site.data.keyword.cloud}} DNS Services is in Experimental Release. At this time the service is available to whitelisted customers only.
{: important}

This section describes how to create various kinds of resource records, and perform other actions around resource records.

## Create resource record of type 'A'
{: #create-an-a-resource-record}


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

## Create resource record of type 'SRV'
{: #create-an-srv-resource-record}

**Request**

```json
curl -X POST \
  https://api.dns-svcs.test.cloud.ibm.com/v1/instances/$INSTANCE_ID/dnszones/$DNSZONE_ID/resource_records \
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

## Create resource record of type 'TXT'
{: #create-a-txt-resource-record}

**Request**

```json
curl -X POST \
  https://api.dns-svcs.test.cloud.ibm.com/v1/instances/$INSTANCE_ID/dnszones/$DNSZONE_ID/resource_records \
  -H "Authorization: $TOKEN" \
  -d '{
	"type": "TXT",
	"name": "txt.example.com",
	"rdata": {
		"txtdata": "txt strings"
	}
}'
```

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

## Create resource record of type 'MX'
{: #create-an-amx-resource-record}

**Request**

```json
curl -X POST \
  https://api.dns-svcs.test.cloud.ibm.com/v1/instances/$INSTANCE_ID/dnszones/$DNSZONE_ID/resource_records \
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

## Create resource record of type 'PTR'
{: #create-a-ptr-resource-record}

**Request**

```json
curl -X POST \
  https://api.dns-svcs.test.cloud.ibm.com/v1/instances/$INSTANCE_ID/dnszones/$DNSZONE_ID/resource_records \
  -H "Authorization: $TOKEN" \
  -d '{
	"type": "PTR",
	"name": "192.168.10.100",
	"rdata": {
	   "ptrdname": "www1.example.com"
	}
}'
```

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

## Create resource record of type 'CNAME'
{: #create-a-cname-resource-record}

**Request**

```json
curl -X POST \
  https://api.dns-svcs.test.cloud.ibm.com/v1/instances/$INSTANCE_ID/dnszones/$DNSZONE_ID/resource_records \
  -H "Authorization: $TOKEN" \
  -d '{
	"type": "CNAME",
	"name": "cname.example.com",
	"rdata": {
	   "cname": "clientinterface.com"
	}
}'
```

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


## Create resource record of type 'AAAA'
{: #create-an-aaaa-resource-record}

**Request**

```json
curl -X POST \
  https://api.dns-svcs.test.cloud.ibm.com/v1/instances/$INSTANCE_ID/dnszones/$DNSZONE_ID/resource_records \
  -H "Authorization: $TOKEN" \
  -d '{
	"type": "AAAA",
	"name": "test.example.com",
	"rdata": {
	   "ip": "8000::2000"
	}
}'
```

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

## Get a resource record
{: #get-a-resource-record}

**Request**

```json
curl -X GET \
  https://api.dns-svcs.test.cloud.ibm.com/v1/instances/$INSTANCE_ID/dnszones/$DNSZONE_ID/resource_records/$RECORD_TAQ \
  -H "Authorization: $TOKEN"
```

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

## List resource records
{: #list-resource-records}

**Request**

```json
curl -X GET \
  https://api.dns-svcs.test.cloud.ibm.com/v1/instances/$INSTANCE_ID/dnszones/$DNSZONE_ID/resource_records \
  -H "Authorization: $TOKEN"
```

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

## Update a resource record
{: #update-a-resource-record}

**Request**

```json
curl -X PUT \
  https://api.dns-svcs.test.cloud.ibm.com/v1/instances/$INSTANCE_ID/dnszones/$ZONE_ID/resource_records/$RECORD_TAG \
  -H "Authorization: $TOKEN" \
  -d '{
	"name":"www", 
	"rdata": {
            "ip":"7.7.7.7"
        }, 
 	"ttl":300
}'
```

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



## Delete a resource record
{: #delete-a-resource-record}

**Request**

```json
curl -X DELETE \
  https://api.dns-svcs.test.cloud.ibm.com/v1/instances/$INSTANCE_ID/dnszones/$DNSZONE_ID/resource_records \
  -H "Authorization: $TOKEN"
```
**Response**

```json
HTTP 204 is returned, no content in response.
```
