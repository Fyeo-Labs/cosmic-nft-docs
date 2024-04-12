# get collection

Get collection details. Replace the collectionId with the collection ID you want to get the details for

*Request*
```
curl 'https://dev.cosmicnft.io/dev/graphql' \
  -H 'accept: */*' \
  -H 'content-type: application/json' \
  --data-raw '{"query":"query Collections {\n  collections(filter: {\n    collectionId: \"992d5a59-9ff5-4234-a9b0-062f2a02f61b\"\n  }) {\n    items {\n      collectionName\n      mintPriceInXahau\n      noOfMintedItems\n      totalItems\n    }\n  }\n}","variables":{},"operationName":"Collections"}'
```

*Response*
```
{
  "data": {
    "collections": {
      "items": [
        {
          "collectionName": "Collection 1",
          "mintPriceInXahau": 1,
          "noOfMintedItems": 0,
          "totalItems": 1
        }
      ]
    }
  }
}
```
