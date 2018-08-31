# 3box-hash-server specification
The implementation of this can be found at [3box-hash-server](https://github.com/uport-project/3box-hash-server.git)

## API Description


### Set 

`POST /hash`

#### Body

```
{
    hash_token: <jwt token containing the hash>
}
```

The `hash_token` is a [DID signed jwt](https://github.com/uport-project/did-jwt.git) of the hash to be published. The payload of the hash_token is:
```
{
    hash: <ipfs hash>
}
```

#### Response

| Status |     Message    |                                                   |
|:------:|----------------|---------------------------------------------------|
| 200    | Ok.            | Hash stored                           |
| 401    | Invalid JWT    | Posted token is invalid (signature, expired, etc) |
| 403    | Missing data   | no `hash` in hash_token                           |
| 500    | Internal Error | Internal Error                                    |

The response data follows the [`jsend`](https://labs.omniti.com/labs/jsend) standard.

#### Response data
```
{
  status: 'success',
  data: {
    hash: <the hash that was accepted>
  }
}
```

### Link an ethereum address to a DID

`POST /link`


#### Body

```
{
    consent_signature: <EIP712 signature>,
    linked_did: <DID>
}
```

The `consent_signature` is a [EIP712 signature](https://eips.ethereum.org/EIPS/eip-712) of a consent message and the DID to be linked. The data of the EIP712 signature is:
```
[{
  type: 'string',
  name: 'I consent to linking my ethereum address to my public profile',
  value: 'did:muport:Qmsd89f7hg0w845hsdd'
}]
```

The address to be linked is recovered from the EIP712 signature.

#### Response

| Status |     Message     |                                                   |
|:------:|-----------------|--------------------------------------------------|
| 200    | Ok.             | Link created and stored                           |
| 401    | Invalid consent | Posted signature is invalid (signature, wrong DID, etc) |
| 403    | Missing data    | no `consent_signature` or `linked_did`             |
| 500    | Internal Error  | Internal Error                                    |

The response data follows the [`jsend`](https://labs.omniti.com/labs/jsend) standard.

#### Response data
```
{
  status: 'success',
  data: {
    did: <the did that was linked>,
    address: <the address that was linked>
  }
}
```

### Get hash for given identity

`GET /hash/{identity}`

Here the `ìdentity` is either a `DID` or an `ethereum address`.

#### Response

| Status |     Message     |                                                   |
|:------:|-----------------|--------------------------------------------------|
| 200    | Ok.             | A hash is returned                           |
| 404    | identity not found    | the DID or ethereum address was not found    |
| 500    | Internal Error  | Internal Error                                    |

The response data follows the [`jsend`](https://labs.omniti.com/labs/jsend) standard.

#### Response data
```
{
  status: 'success',
  data: {
    hash: <the hash associated with the identity>
  }
}
```


### Delete hash
TBD

### Delete link
TBD

