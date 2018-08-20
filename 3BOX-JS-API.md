# 3box-js api specification
The implementation of this can be found at [3box-js](https://github.com/uport-project/3box-js)

## API Description


<a name="3Box"></a>

## 3Box
**Kind**: global class

* [3Box](#3Box)
    * [new 3Box(muDID)](#new_3Box_new)
    * _instance_
        * [.private.get(key)](#3Box+get) ⇒ <code>String</code>
        * [.private.set(key, value)](#3Box+set) ⇒ <code>Boolean</code>
        * [.private.remove(key)](#3Box+remove) ⇒ <code>Boolean</code>
        * [.profile.get(key)](#3Box+profileGet) ⇒ <code>String</code>
        * [.profile.set(key, value)](#3Box+profileSet) ⇒ <code>Boolean</code>
        * [.profile.remove(key)](#3Box+profileRemove) ⇒ <code>Boolean</code>
    * _static_
        * [.openBox(address)](#3Box.open) ⇒ [<code>3Box</code>](#3Box)
        * [.getPublicProfile(address)](#3Box.getPublicProfile) ⇒ [<code>3Box</code>](#3Box)
        * [.getPublicActivity(address)](#3Box.getPublicActivity) ⇒ [<code>3Box</code>](#3Box)

<a name="new_3Box_new"></a>

### new 3Box(muDID)
Instantiates a 3box

**Returns**: [<code>3Box</code>](#3Box) - self

| Param | Type | Description |
| --- | --- | --- |
| muDID | <code>MuPort</code> | A MuPort DID instance |

<a name="3Box+get"></a>

### 3box.private.get(key) ⇒ <code>String</code>
Get the value of the given key

**Kind**: instance method of [<code>3Box</code>](#3Box)
**Returns**: <code>String</code> - the value associated with the key

| Param | Type | Description |
| --- | --- | --- |
| key | <code>String</code> | the key |

<a name="3Box+set"></a>

### 3box.private.set(key, value) ⇒ <code>Boolean</code>
Set a value for the given key in the private data store

**Kind**: instance method of [<code>3Box</code>](#3Box)
**Returns**: <code>Boolean</code> - true if successful

| Param | Type | Description |
| --- | --- | --- |
| key | <code>String</code> | the key |
| value | <code>String</code> | the value |

<a name="3Box+remove"></a>

### 3box.private.remove(key) ⇒ <code>Boolean</code>
Remove the value for the given key in the private data store

**Kind**: instance method of [<code>3Box</code>](#3Box)
**Returns**: <code>Boolean</code> - true if successful

| Param | Type | Description |
| --- | --- | --- |
| key | <code>String</code> | the key |

<a name="3Box+profileGet"></a>

### 3box.profile.get(key) ⇒ <code>Boolean</code>
Get the value for the given key in the public profile

**Kind**: instance method of [<code>3Box</code>](#3Box)
**Returns**: <code>String</code> - the value associated with the key

| Param | Type | Description |
| --- | --- | --- |
| key | <code>String</code> | the key |

<a name="3Box+profileSet"></a>

### 3box.profile.set(key, value) ⇒ <code>Boolean</code>
Set a value for the given key in the public profile

**Kind**: instance method of [<code>3Box</code>](#3Box)
**Returns**: <code>Boolean</code> - true if successful

| Param | Type | Description |
| --- | --- | --- |
| key | <code>String</code> | the key |
| value | <code>String</code> | the value |

<a name="3Box+profileRemove"></a>

### 3box.profile.remove(key) ⇒ <code>Boolean</code>
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
