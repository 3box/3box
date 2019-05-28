# Contacts
A list of contacts is comprised of contact objects. For a contact object, we're following the Person schema from https://schema.org. The minimum viable contact object must contain at least one `identifier`.

**Contact Object**

    {
      "@context": "http://schema.org/",
      "@type": "Person",
      "name": "Mollie Narwhal",
      "description": "We built open source code and community at 3Box",
      "identifier": [
        {
          "@type": "PropertyValue",
          "name": "DID",
          "value": "did:3:zhf02344f2d32dawe"
        },
        {
         "@type": "PropertyValue",
          "name": "Ethereum",
          "PropertyID": "chainId_1"
          "value": "0x123456781234567812345678123"
        },
      ]
    }


## 3Box Followers
In the [3Box hub application](https://3box.io) and in various other 3Box components, we support public followers. This allows users to publicly "follow" other addresses (or profiles) by adding them to their public profile. Below, find the slim followers object, based on the full contacts object outlined above. A 3Box follower must contain at least one `identifier`, either `Ethereum` or `DID`.

    {
      "@context": "http://schema.org/",
      "@type": "Person",
      "identifier": [
        {
          "@type": "PropertyValue",
          "name": "DID",
          "value": "did:3:zhf02344f2d32dawe"
        },
        {
         "@type": "PropertyValue",
          "name": "Ethereum",
          "PropertyID": "chainId_1"
          "value": "0x123456781234567812345678123"
        },
      ]
    }
