# Batch Operations

## Processing Similar Resources
An operation that needs to process several similar resource in bulk **SHOULD** use a collection resource with the appropriate HTTP Request Method. When processing existing resource the request message body **MUST** contain the URLs of the respective resources being processed.

#### Example
##### Create Multiple Orders at Once

```
POST /orders
Content-Type: application/json

{
  "order": [
    {
      "item_count": 42
    },
    {
      "item_count": 2
    }
  ]
}
```


##### Update Multiple Orders at Once
> NOTE: The self link relation clearly identifies the existing resource being edited.

```
PATCH /orders
Content-Type: application/json

{
  "order": [
    {
      "_links": {
        "self": { "href": "/order/1"}
      },
      "item_count": 42
    },
    {
      "_links": {
        "self": { "href": "/order/2"}
      },      
      "item_count": 2
    }
  ]
}
```

## Results of Bulk Operation
Every bulk operation **MUST** be atomic. 

> _The server must implement bulk requests as atomic. If the request is for creating 10 addresses, the server should create all 10 addresses before returning a successful response code. The server should not commit changes partially in the case of failures._


## DO NOT USE "POST Tunneling"
Every API **MUST** avoid tunneling multiple HTTP Request using one POST request. Instead provide an application-specific resource to process the batch request.







