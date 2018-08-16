# 3box-data-storage-scheme
The implementation of this can be found at [3box-data-storage-api](https://github.com/uport-project/3box-3box-data-storage-api.git)

## API Description

The storage scheme is a wrapper of some of the [orbitdb](https://github.com/orbitdb/orbit-db) types of databases available. In particular we are interested in `keyvalue` and `feed`

## Key-Value Store

`POST /datastore`

### Body

```
{
    data: <jwt token containing the key/value pair to store>
}
```

The `data` field is a [DID signed jwt](https://github.com/uport-project/did-jwt.git) of the data that wants to be stored. The payload of the hash_token is:
```
{
    key: <key to the data to store>,
    value: <the actual value>,
}
```

#### Response

| Status |     Message    |                                                   |
|:------:|----------------|---------------------------------------------------|
| 200    | Ok.            | Key/Value pair stored                           |
| 401    | Invalid JWT    | Posted token is invalid (signature, expired, etc) |
| 403    | Missing data   | no `key` or `value` in hash_token                           |
| 500    | Internal Error | Internal Error

`GET /datastore`

### Body

```
{
    data: <jwt token containing the key to retrieve>
}
```

The `data` field is a [DID signed jwt](https://github.com/uport-project/did-jwt.git) of the data that wants to be retrieved. The payload of the `data` field is:
```
{
    key: <key to the data to retrieve>
}
```

#### Response

| Status |     Message    |                                                   |
|:------:|----------------|---------------------------------------------------|
| 200    | Ok.            | A value is retrieved                           |
| 401    | Invalid JWT    | Posted token is invalid (signature, expired, etc) |
| 403    | Missing data   | No `key` in data
| 404    | Not found   | No value associated with that key in the datastore
| 500    | Internal Error | Internal Error


`DELETE /datastore`

### Body

```
{
    data: <jwt token containing the key to delete>
}
```

The `data` field is a [DID signed jwt](https://github.com/uport-project/did-jwt.git) of the data that wants to be deleted. The payload of the `data` field is:
```
{
    key: <key to the data to delete>
}
```
#### Response

| Status |     Message    |                                                   |
|:------:|----------------|---------------------------------------------------|
| 200    | Ok.            | Key/Value pair removed                           |
| 401    | Invalid JWT    | Posted token is invalid (signature, expired, etc) |
| 403    | Missing data   | No `key` in data
| 404    | Not found   | No value associated with that key in the datastore
| 500    | Internal Error | Internal Error

## Feed


`POST /feed`

### Body

```
{
    data: <jwt token containing the feed data to store>
}
```

The `data` field is a [DID signed jwt](https://github.com/uport-project/did-jwt.git) of the data that wants to be stored.


#### Response

| Status |     Message    |                                                   |
|:------:|----------------|---------------------------------------------------|
| 200    | Ok.            | Feed entry is stored                          |
| 401    | Invalid JWT    | Posted token is invalid (signature, expired, etc) |
| 500    | Internal Error | Internal Error


The response data follows the [`jsend`](https://labs.omniti.com/labs/jsend) standard.

#### Response data
```
{
  status: 'success',
  data: {
    hash: <the hash of the feed data>
  }
}
```

`GET /datastore`

### Body

```
{
    data: <jwt token containing the hash of the feed data to retrieve>
}
```

The `data` field is a [DID signed jwt](https://github.com/uport-project/did-jwt.git) of the data that wants to be retrieved. The payload of the `data` field is:
```
{
    hash: <hash of the feed data to retrieve>
}
```

#### Response

| Status |     Message    |                                                   |
|:------:|----------------|---------------------------------------------------|
| 200    | Ok.            | A data object is returned                           |
| 401    | Invalid JWT    | Posted token is invalid (signature, expired, etc) |
| 403    | Missing data   | No `hash` in data
| 404    | Not found   | No data associated with that hash in the feed store
| 500    | Internal Error | Internal Error


`DELETE /datastore`

### Body

```
{
    data: <jwt token containing the hash of the data to delete>
}
```

The `data` field is a [DID signed jwt](https://github.com/uport-project/did-jwt.git) of the data that wants to be deleted. The payload of the `data` field is:
```
{
    hash: <hash of the feed data to delete>
}
```
#### Response

| Status |     Message    |                                                   |
|:------:|----------------|---------------------------------------------------|
| 200    | Ok.            | Data is deleted from the feed store                           |
| 401    | Invalid JWT    | Posted token is invalid (signature, expired, etc) |
| 403    | Missing data   | No `hash` in data
| 404    | Not found   | No data associated with that hash in the feed store
| 500    | Internal Error | Internal Error

