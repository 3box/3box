# 3box-root-hash-tracker specification
The implementation of this can be found at [3box-js](https://github.com/uport-project/3box-js)

## API Description


<a name="3Box"></a>

## 3Box
**Kind**: global class

* [3Box](#3Box)
    * [new 3Box(muDID)](#new_3Box_new)
    * _instance_
        * [.getPrivate(key)](#3Box+getPrivate) ⇒ <code>String</code>
        * [.setPrivate(key, value)](#3Box+setPrivate) ⇒ <code>Boolean</code>
        * [.removePrivate(key)](#3Box+removePrivate) ⇒ <code>Boolean</code>
        * [.setToProfile(key, value)](#3Box+setToProfile) ⇒ <code>Boolean</code>
        * [.removeFromProfile(key, value)](#3Box+setToProfile) ⇒ <code>Boolean</code>
    * _static_
        * [.openBox(address)](#3Box.open) ⇒ [<code>3Box</code>](#3Box)
        * [.getPublicProfile(address)](#3Box.getProfile) ⇒ [<code>3Box</code>](#3Box)
        * [.getPublicActivity(address)](#3Box.getPublicActivity) ⇒ [<code>3Box</code>](#3Box)

<a name="new_3Box_new"></a>

### new 3Box(muDID)
Instantiates a 3box

**Returns**: [<code>3Box</code>](#3Box) - self

| Param | Type | Description |
| --- | --- | --- |
| muDID | <code>MuPort</code> | A MuPort DID instance |

<a name="3Box+getPrivate"></a>

### 3box.getAll() ⇒ <code>Object</code>
Get all of the items in the 3box in the private data store

**Kind**: instance method of [<code>3Box</code>](#3Box)
**Returns**: <code>Object</code> - an object containing all items
<a name="3Box+setPrivate"></a>

### 3box.setPrivate(key, value) ⇒ <code>Boolean</code>
Set a value for the given key in the private data store

**Kind**: instance method of [<code>3Box</code>](#3Box)
**Returns**: <code>Boolean</code> - true if successful

| Param | Type | Description |
| --- | --- | --- |
| key | <code>String</code> | the key |
| value | <code>String</code> | the value |

<a name="3Box+removePrivate"></a>

### 3box.removePrivate(key) ⇒ <code>Boolean</code>
Remove the value for the given key in the private data store

**Kind**: instance method of [<code>3Box</code>](#3Box)
**Returns**: <code>Boolean</code> - true if successful

| Param | Type | Description |
| --- | --- | --- |
| key | <code>String</code> | the key |

### 3box.setToProfile(key, value) ⇒ <code>Boolean</code>
Set a value for the given key in the public profile

**Kind**: instance method of [<code>3Box</code>](#3Box)
**Returns**: <code>Boolean</code> - true if successful

| Param | Type | Description |
| --- | --- | --- |
| key | <code>String</code> | the key |
| value | <code>String</code> | the value |

<a name="3Box+removeFromProfile"></a>

### 3box.removeFromProfile(key) ⇒ <code>Boolean</code>
Remove the value for the given key in the public profile

**Kind**: instance method of [<code>3Box</code>](#3Box)
**Returns**: <code>Boolean</code> - true if successful

| Param | Type | Description |
| --- | --- | --- |
| key | <code>String</code> | the key |

<a name="3Box.open"></a>

### 3Box.open(address) ⇒ [<code>3Box</code>](#3Box)
Opens the user space associated with the given address

**Kind**: static method of [<code>3Box</code>](#3Box)
**Returns**: [<code>3Box</code>](#3Box) - the 3box instance for the given address

| Param | Type | Description |
| --- | --- | --- |
| address | <code>String</code> | an ethereum address |

<a name="3Box.getPublicProfile"></a>

### 3Box.getPublicProfile(address) ⇒ [<code>3Box</code>](#3Box)
Returns the public profile associated with the given address

**Kind**: static method of [<code>3Box</code>](#3Box)
**Returns**: [<code>Object</code>](#3Box) - the public profile of the given address

| Param | Type | Description |
| --- | --- | --- |
| address | <code>String</code> | an ethereum address |

<a name="3Box.getPublicActivity"></a>

### 3Box.getPublicActivity(address) ⇒ [<code>3Box</code>](#3Box)
Returns the public activity associated with the given address

**Kind**: static method of [<code>3Box</code>](#3Box)
**Returns**: [<code>3Box</code>](#3Box) - the public activity of the given address

| Param | Type | Description |
| --- | --- | --- |
| address | <code>String</code> | an ethereum address |
