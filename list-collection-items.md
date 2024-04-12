# list collection items

- Get list of items in a collection which were already minted
- This API works without JWT token in header
- You can control what fields you want to see in the response. Please check our [GraphQL playground](https://dev.cosmicnft.io/dev/graphql) for details of fields that are available to be retrieved using this API
- This endpoint returns data in paginated way. You have to use the cursor to continue to pull more items in a collection

*Request*
```
curl 'https://dev.cosmicnft.io/dev/graphql' \
  -H 'accept: */*' \
  -H 'content-type: application/json' \
  --data-raw '{"query":"query Collections {\n  collectionItems(filter: {\n    collectionId: \"bd2a879e-1793-4d36-9209-1a4e5029d473\"\n  }) {\n    items {\n      collectionId\n      itemId\n    }\n    pageInfo {\n      cursor\n    }\n  }\n}","operationName":"Collections"}'
```

*Response*
```
{
  "data": {
    "collectionItems": {
      "items": [
        {
          "collectionId": "bd2a879e-1793-4d36-9209-1a4e5029d473",
          "itemId": "12f63ef6-c1b4-4d53-bda8-236e23bbcd79"
        }
      ],
      "pageInfo": {
        "cursor": null
      }
    }
  }
}
```
