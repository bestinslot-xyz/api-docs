---
description: Endpoints related to Bitmap.
---

# Bitmap

Endpoints' API-Key-Tier availabilities are written for each endpoint.

**To use on testnet4/signet, use your current api-key and send the request to `https://testnet.api.bestinslot.xyz` / `https://signet_api.bestinslot.xyz`**

## Get Bitmap Holders

_<mark style="color:blue;">Included in: Basic, Pro, Dedicated</mark>_

<mark style="color:blue;">`GET`</mark> `https://api.bestinslot.xyz/v3/bitmap/holders`

Returns an array with holder information. Each entry has a wallet address and collected inscription ids.

Sample query: https://api.bestinslot.xyz/v3/bitmap/holders?sort\_by=wallet\_addr\&order=asc\&offset=0\&count=100

#### Query Parameters

| Name                                     | Type   | Description                   |
| ---------------------------------------- | ------ | ----------------------------- |
| sort\_by                                 | string | (optional) "wallet\_addr"     |
| order                                    | string | (optional) "asc", "desc"      |
| offset<mark style="color:red;">\*</mark> | int    | (optional) 0 <= offset        |
| count<mark style="color:red;">\*</mark>  | int    | (optional) 20 <= count <= 100 |

{% tabs %}
{% tab title="200: OK Success" %}
```json
{
    "data": [
        {
            "wallet": "12ufzRLA89ZyLPTe6HCUnVGRtdNfr8tYXp",
            "inscription_ids": [
                "5e7989591908aa5e1874545518b4b2d9ccfbde83f40a94340cc5fbd5d923b981i0",
                "b5eced1df647a5a55c2753d44dfb8976a5a7c6c0035f68c76c6a96bb60e14700i0",
                "689616aeeb568d3e93fae34563b2134b81fa46ebc58b32b45b26332b945f8569i0",
                "c7117a8e524b657b3f37b9d42d7fce5d62a920307e569448131cd3ab9cb2cb43i0",
                "d9875cf906b853a3204270bbc8f53a8054716ba3ffdc2da4d2a87e77631c473di0"
            ]
        },
        ...
    ],
    "block_height": 795035
}
```
{% endtab %}

{% tab title="429: Too Many Requests Rate limit exceeded" %}

{% endtab %}
{% endtabs %}



## Get Bitmap Inscriptions

_<mark style="color:blue;">Included in: Basic, Pro, Dedicated</mark>_

<mark style="color:blue;">`GET`</mark> `https://api.bestinslot.xyz/v3/bitmap/inscriptions`

Returns ordered list of bitmap inscriptions.

Sample query: https://api.bestinslot.xyz/v3/bitmap/inscriptions?sort\_by=inscr\_num\&order=asc\&offset=100\&count=100

<mark style="color:orange;">**NOTE:**</mark> <mark style="color:orange;"></mark><mark style="color:orange;">last\_sale\_price is only available on Pro Tier.</mark>

#### Query Parameters

| Name                                       | Type   | Description        |
| ------------------------------------------ | ------ | ------------------ |
| sort\_by<mark style="color:red;">\*</mark> | string | inscr\_num         |
| order<mark style="color:red;">\*</mark>    | string | asc, desc          |
| offset<mark style="color:red;">\*</mark>   | int    | 0 <= offset        |
| count<mark style="color:red;">\*</mark>    | int    | 20 <= count <= 100 |

{% tabs %}
{% tab title="200: OK Success" %}
```json
{
    "data": [
        {
            "bitmap_number": 0,
            "inscription_id": "86539aff946c437af8088955827b7e6ff48fc6192836d4071b697b5359b7a732i0",
            "inscription_number": 10423123,
            "owner_wallet_addr": "bc1p7hf8x2q2zal4v64c2h34qheyz4zk8zgnv767ygkkrd5dhg9zackq4rmvhd",
            "last_transfer_block_height": 792435,
            "genesis_height": 792435,
            "last_sale_price": null,
            "content_url": "https://bis-ord-content.fra1.cdn.digitaloceanspaces.com/ordinals/86539aff946c437af8088955827b7e6ff48fc6192836d4071b697b5359b7a732i0",
            "bis_url": "https://bestinslot.xyz/ordinals/inscription/86539aff946c437af8088955827b7e6ff48fc6192836d4071b697b5359b7a732i0"
        },
        ...
    ],
    "block_height": 799055
}
```
{% endtab %}

{% tab title="429: Too Many Requests Rate limit exceeded" %}

{% endtab %}
{% endtabs %}



## Get Bitmap Sales Information

_<mark style="color:blue;">Included in: Pro, Dedicated</mark>_

<mark style="color:blue;">`GET`</mark> `https://api.bestinslot.xyz/v3/bitmap/sales_info`

Returns sales and volume information about bitmaps.

Sample query: https://api.bestinslot.xyz/v3/bitmap/sales\_infomarketplace\_type=magiceden

#### Query Parameters

| Name              | Type   | Description                                                                                                 |
| ----------------- | ------ | ----------------------------------------------------------------------------------------------------------- |
| marketplace\_type | string | Optional parameter to filter only by a given marketplace. You can find the allowed types on Constants Page. |

{% tabs %}
{% tab title="200: OK Success" %}
```json
{
    "data": {
        "vol_3h": "5582294",
        "vol_6h": "21472011",
        "vol_9h": "34006304",
        "vol_12h": "36548463",
        "vol_1d": "51050633",
        "vol_3d": "91950108",
        "vol_7d": "165391876",
        "vol_30d": "755204897",
        "vol_total": "9207676876",
        "sale_count": 137473,
        "marketplace": "all"
    },
    "block_height": 814057
}
```
{% endtab %}

{% tab title="429: Too Many Requests Rate limit exceeded" %}

{% endtab %}

{% tab title="403: Forbidden Invalid API-Key" %}

{% endtab %}
{% endtabs %}



## Get Bitmap Market Information

_<mark style="color:blue;">Included in: Pro, Dedicated</mark>_

<mark style="color:blue;">`GET`</mark> `https://api.bestinslot.xyz/v3/bitmap/market_info`

Returns market information like marketcap, listed count, floor price about bitmaps.

Sample query: https://api.bestinslot.xyz/v3/bitmap/market\_info

{% tabs %}
{% tab title="200: OK Success" %}
```json
{
    "data": {
        "listed_count": 31279,
        "floor_price": 73344,
        "floor_price_ordswap": null,
        "floor_price_magiceden": 79560,
        "floor_price_ordinalswallet": 73344,
        "floor_price_gammaio": null,
        "floor_price_ordynals": null,
        "floor_price_unisat": 75375,
        "floor_price_ordinalsmarket": 15000000,
        "floor_price_okx": 76000,
        "supply": 849818,
        "marketcap": 62329051392
    },
    "block_height": 849817
}
```
{% endtab %}

{% tab title="429: Too Many Requests Rate limit exceeded" %}

{% endtab %}

{% tab title="403: Forbidden Invalid API-Key" %}

{% endtab %}
{% endtabs %}



## Get Bitmap Listings

_<mark style="color:blue;">Included in: Pro, Dedicated</mark>_

<mark style="color:blue;">`GET`</mark> `https://api.bestinslot.xyz/v3/bitmap/listings`

Returns ordered list of listings of bitmaps.

Sample query: https://api.bestinslot.xyz/v3/bitmap/listings?sort\_by=min\_price\&order=asc\&offset=0\&count=100

#### Query Parameters

| Name                                       | Type   | Description                                                                                                                                           |
| ------------------------------------------ | ------ | ----------------------------------------------------------------------------------------------------------------------------------------------------- |
| sort\_by<mark style="color:red;">\*</mark> | string | min\_price, ordswap\_price, magiceden\_price, ordinalswallet\_price, gammaio\_price, odynals\_price, unisat\_price, ordinalsmarket\_price, okx\_price |
| order<mark style="color:red;">\*</mark>    | string | asc, desc                                                                                                                                             |
| offset<mark style="color:red;">\*</mark>   | int    | 0 <= offset <= 5k                                                                                                                                     |
| count<mark style="color:red;">\*</mark>    | int    | 20 <= count <= 100                                                                                                                                    |

{% tabs %}
{% tab title="200: OK Success" %}
```json
{
    "data": [
        {
            "inscription_id": "013dcd2c02ff459aa240a9e3a09d6e0203c9332a3ad691be7297bcb62d635cb4i0",
            "min_price": 30000,
            "ordswap_price": null,
            "magiceden_price": null,
            "ordinalswallet_price": 30000,
            "gammaio_price": null,
            "nostr_price": null,
            "odynals_price": null,
            "unisat_price": null,
            "ordinalsmarket_price": null,
            "okx_price": null,
            "owner_wallet_addr": "bc1p28m2g5rvyjjc2a625thtsv7snv4gpqv9ens5vz5kftx2smhzjn5qawq0fy"
        },
        ...
    ],
    "block_height": 803265
}
```
{% endtab %}

{% tab title="429: Too Many Requests Rate limit exceeded" %}

{% endtab %}

{% tab title="403: Forbidden Invalid API-Key" %}

{% endtab %}
{% endtabs %}



## Get Bitmap Activity

_<mark style="color:blue;">Included in: Pro, Dedicated</mark>_

<mark style="color:blue;">`GET`</mark> `https://api.bestinslot.xyz/v3/bitmap/activity`

Returns ordered list of inscribes, sales and transfers of bitmaps.

<mark style="color:orange;">NOTE: Use last\_new\_satpoint to continue fetching the activity from where you've left off. new\_satpoint uniquely addresses a single inscription transfer, so by setting order to asc, and last\_new\_satpoint to the latest new\_satpoint value that you've received, you can retrieve the new activities.</mark>

Sample query: https://api.bestinslot.xyz/v3/bitmap/activity?activity\_filter=7\&sort\_by=ts\&order=asc\&offset=0\&count=100\&last\_new\_satpoint=cc9f10dda7c6e03637ed8205f33067f6d0b20520bb082f500ea33edd5a10ebc5:2:0

#### Query Parameters

| Name                                               | Type   | Description                                                                                                                  |
| -------------------------------------------------- | ------ | ---------------------------------------------------------------------------------------------------------------------------- |
| sort\_by<mark style="color:red;">\*</mark>         | string | ts                                                                                                                           |
| order<mark style="color:red;">\*</mark>            | string | asc, desc                                                                                                                    |
| offset<mark style="color:red;">\*</mark>           | int    | 0 <= offset <= 5k                                                                                                            |
| count<mark style="color:red;">\*</mark>            | int    | 20 <= count <= 100                                                                                                           |
| activity\_filter<mark style="color:red;">\*</mark> | int    | <p>1 -> inscribed<br>2 -> transferred<br>4 -> sold<br>combine with or operator (e.g. sold &#x26; transferred: 2 | 4 = 6)</p> |
| last\_new\_satpoint                                | string | (optional) use this with offset 0 to continue from a known transfer                                                          |

{% tabs %}
{% tab title="200: OK Success" %}
```json
{
    "data": [
        {
            "inscription_id": "10490d6e63cdced2810011dcbb0952e26ca7a7bc609167487b76f567306dbfd5i0",
            "from_wallet": "bc1pn4zg6zwk256tlhgkxlj2jn6khnrtuynafw9cz6lrp6wvgmywkmusn6m8xd",
            "to_wallet": "bc1p4kdgatpw9sdawnjzt206yyu33uhxnfpnv476td8m0tt8rznnvxkqk49rvh",
            "block_height": 814057,
            "sale_price": 21242,
            "new_satpoint": "31226b1ea0acc7a46ff7b1a86745e88dab759deaf50836b62d044d5f17801bad:1:0",
            "ts": "2023-10-27T11:47:28.000Z",
            "marketplace_type": "magiceden",
            "tx_id": "31226b1ea0acc7a46ff7b1a86745e88dab759deaf50836b62d044d5f17801bad"
        },
        ...
    ],
    "block_height": 795035
}
```
{% endtab %}

{% tab title="429: Too Many Requests Rate limit exceeded" %}

{% endtab %}

{% tab title="403: Forbidden Invalid API-Key" %}

{% endtab %}
{% endtabs %}
