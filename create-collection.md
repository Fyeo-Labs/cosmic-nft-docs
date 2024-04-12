# create collection

Follow these steps to create collection

- Get a token following [create jwt token](./create-jwt-token.md)
- Get a temporary spot to upload your image

*Request*
```
curl 'https://dev.cosmicnft.io/dev/graphql' \
  -H 'accept: */*' \
  -H 'authorization: Bearer <your jwt token>' \
  -H 'content-type: application/json' \
  --data-raw '{"query":"\n  mutation createPresignedUrl {\n    createPresignedUrl {\n      url\n      key\n    }\n  }\n","operationName":"createPresignedUrl"}'
```

*Response*
```
{
    "data": {
        "createPresignedUrl": {
            "url": "https://cosmicnft-storage-dev.s3.us-east-1.amazonaws.com/nft/rMSMWjbJXbuC8f1KYT5KxnvPeBUVERf9y2/2497f53f-c7c3-40dd-b572-27c262ffcd15?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LHIXNIVUNYSQ3%2F20240412%2Fus-east-1%2Fs3%2Faws4_request&X-Amz-Date=20240412T025927Z&X-Amz-Expires=900&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEBsaCXVzLWVhc3QtMSJIMEYCIQD%2B%2BwsaZvAz%2FFQHyySyCb8sH8F53BQg9Un1bbeargQNGgIhAJTkSXM6jeO%2BaeNUFoFMMb2V9byuxJaaPeEW7HKPlRYTKvICCFQQABoMNjM3NDIzNTM1NTc4IgxXOmJCT%2Byqmww2PnwqzwL3pSBadba3LwsaWu7T3nqsHP0nEU%2BecBU4nvRKadusp0FiFUgosAjNgCypLp7v5Lj%2Fmxt14X%2F62V%2B3mrlQY%2B1xHWpu3vchMJh%2BeCBhpAfK7uY%2BW7OzjCJj2vzUgpwfPbtLB65c%2F9YE76WknCBsLO66aZXU%2FF3EO2IqcmNU0w%2B2REM%2B4YH7Uu66geIjbtI9TQMtAQFkHDclz5Mf1988gliqWGOGBn3iVfDH%2FLgNs7niQ7eq6FpMWQYU8eBpB2Qggzc9QJbOcAe78I0bvyh9kG9VPgDtCd4sSz05W2ChCVaODZaYF7JcdtD8zQ%2BwpC4c5kUJtECHAlWobe5qk6UxPPXrMvQJ3WJebYW7rDAXNK67WnIkLzloSmcJXn%2BDa7u%2BeL6x2L6qdYUJ4xBEjBUWx2BUs6AoOgi18BD%2FC1%2BJ%2FZcH2kkrGSJqIaAz5v0w77TZPTCLx%2BKwBjqdAb5ZE5kmVFJF9G7k16lOCayJptWf9YmPzNdVT%2FfhPACabIU8bnlfwOayyjykMn%2FIqtHYFD6BaBUOcxoSIgh02CDRcwITqjomycRDbTBMHzXE4JJq4%2F3ZerSkhxVF93Q0sDtg9yqod8aFfv7vFZJ40C8abPF2lJ0ayN17ZdTptrSMgiG7gXXhvZiN%2F9q4FVZQWwq4XkuFkDZMVic1HHw%3D&X-Amz-Signature=e3016c8c93351615b863df03f0f0259a959e5b0ee5a67b3b215b9323a29538f3&X-Amz-SignedHeaders=host",
            "key": "nft/rMSMWjbJXbuC8f1KYT5KxnvPeBUVERf9y2/2497f53f-c7c3-40dd-b572-27c262ffcd15"
        }
    }
}
```

- Response above returns a JSON which has `url` field. Do a `PUT` call to that URL with the image file you want to upload
```
curl --request PUT --upload-file "/path/to/your/image/file.png" <replace this with the content of `url` field from above>
```

- Repeat the above step for each image you want to upload
- Keep track of all the `key` for each image uploaded. You will need them to create a collection
- Do the above steps one more time for a thumbnail for your collection. Attach thumbnail image this time
- create the collection using following command. Replace `collection name`, `collection description`, `minting price`, `<thumbnail key>`, `<royalty>`. `<thumbnail key>` should be `key` generated above for the thumbnail upload
  
*Request*
```
curl 'https://dev.cosmicnft.io/dev/graphql' \
  -H 'accept: */*' \
  -H 'authorization: Bearer <your jwt token>' \
  -H 'content-type: application/json' \
  --data-raw $'{"query":"\\n  mutation createCollection($record: ServerCollectionCreateInput\u0021) {\\n    createCollection(record: $record) {\\n      collectionId\\n    }\\n  }\\n","variables":{"record":{"collectionName": <collection name>,"collectionDescription": <collection description>,"mintPriceInXahau": <minting price>,"thumbNailUrl":"<thumbail key>","royalty":<royalty>}},"operationName":"createCollection"}'
```

*Response*
```
{
    "data": {
        "createCollection": {
            "collectionId": "17932463-6d46-4300-9ec6-07e8ee5080b8"
        }
    }
}
```

- create collection items using the following command. Replace `<collection id>` with value of `collectionId` return in the previous API call, `<collection item name>` with the name of the collection item (recommended to name it as `Collection name - Item #number`), `<item image key>` with the `key` of the image obtain in the first step. You can add ad many attributes as you want in the `attributes` field. It has to be valid JSON array object with `name` and `value` in each object.
```
curl 'https://dev.cosmicnft.io/dev/graphql' \
  -H 'accept: */*' \
  -H 'authorization: Bearer <your-jwt-token>' \
  -H 'content-type: application/json' \
  --data-raw $'{"query":"\\n  mutation createCollectionItem($record: ServerCollectionItemCreateInput\u0021) {\\n    createCollectionItem(record: $record) {\\n      itemId\\n    }\\n  }\\n","variables":{"record":{"collectionId": "<collection id>","itemName":"<collection item name>","url":"<item image key>","attributes":[{"name":"1","value":"1"}]}},"operationName":"createCollectionItem"}'
```