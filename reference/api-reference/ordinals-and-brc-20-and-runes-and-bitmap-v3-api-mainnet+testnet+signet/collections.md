---
description: Endpoints related to Ordinals Collections.
---

# Collections

Endpoints' API-Key-Tier availabilities are written for each endpoint.

**NOTE:** sub1k and sub10k meta-collection information can be retrieved by using these as slug.

**To use on testnet4/signet, use your current api-key and send the request to `https://testnet.api.bestinslot.xyz` / `https://signet_api.bestinslot.xyz`**

## Get collections

_<mark style="color:blue;">Included in: Basic, Pro, Dedicated</mark>_

<mark style="color:blue;">`GET`</mark> `https://api.bestinslot.xyz/v3/collection/collections`

Returns ordered list of collections with detailed information about them.

Sample query: https://api.bestinslot.xyz/v3/collection/collections?sort\_by=median\_number\&order=asc\&offset=100\&count=100

<mark style="color:orange;">**NOTE:**</mark> <mark style="color:orange;"></mark><mark style="color:orange;">inscription\_icon\_id may be a URL for some collections</mark>

<mark style="color:orange;">**NOTE:**</mark> <mark style="color:orange;"></mark><mark style="color:orange;">listed\_count, floor\_price, floor\_price\_ordswap, floor\_price\_magiceden, floor\_price\_ordinalswallet, floor\_price\_gammaio, floor\_price\_ordynals, floor\_price\_ordinalsmarket, floor\_price\_okx, vol\_24h\_in\_btc, vol\_7d\_in\_btc, sale\_cnt\_7d, vol\_total\_in\_btc, sale\_cnt\_total, marketcap is only available on Pro Tier.</mark>

#### Query Parameters

| Name                                       | Type   | Description                                                                                                                                                                                                                                                                                                                                                                        |
| ------------------------------------------ | ------ | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| sort\_by<mark style="color:red;">\*</mark> | string | <p>supply, min_number, median_number, max_number</p><p><br>PRO TIER:<br>listed_count, floor_price, floor_price_ordswap, floor_price_magiceden, floor_price_ordinalswallet, floor_price_gammaio, floor_price_ordynals, floor_price_ordinalsmarket, floor_price_unisat, floor_price_okx, vol_24h_in_btc, vol_7d_in_btc, sale_cnt_7d, vol_total_in_btc, sale_cnt_total, marketcap</p> |
| order<mark style="color:red;">\*</mark>    | string | asc, desc                                                                                                                                                                                                                                                                                                                                                                          |
| offset<mark style="color:red;">\*</mark>   | int    | 0 <= offset                                                                                                                                                                                                                                                                                                                                                                        |
| count<mark style="color:red;">\*</mark>    | int    | 20 <= count <= 100                                                                                                                                                                                                                                                                                                                                                                 |

{% tabs %}
{% tab title="200: OK Success" %}
```json
{
    "data": [
        {
            "name": "Quantum Cats",
            "slug": "quantum_cats",
            "inscription_icon_id": "https://creator-hub-prod.s3.us-east-2.amazonaws.com/ord-taproot_wizards_presents_pfp_1706542390359.png",
            "icon_url": "https://creator-hub-prod.s3.us-east-2.amazonaws.com/ord-taproot_wizards_presents_pfp_1706542390359.png",
            "icon_render_url": null,
            "bis_url": "https://bestinslot.xyz/ordinals/collection/quantum_cats",
            "supply": "3333",
            "min_number": 53785860,
            "median_number": 53788086,
            "max_number": 53790617,
            "listed_count": 132,
            "floor_price": 12136980,
            "floor_price_ordswap": null,
            "floor_price_magiceden": 12136980,
            "floor_price_ordinalswallet": null,
            "floor_price_gammaio": null,
            "floor_price_ordynals": null,
            "floor_price_unisat": null,
            "floor_price_ordinalsmarket": 199000000,
            "floor_price_okx": 20000000,
            "vol_3h_in_btc": 0.20895894,
            "vol_24h_in_btc": 0.20895894,
            "vol_7d_in_btc": 16.14854946,
            "vol_30d_in_btc": 92.46122358,
            "sale_cnt_7d": 139,
            "vol_total_in_btc": 1683.87253749,
            "sale_cnt_total": 6352,
            "marketcap": 40452554340
        },
        ...
    ],
    "block_height": 889392
}
```
{% endtab %}

{% tab title="429: Too Many Requests Rate limit exceeded" %}

{% endtab %}
{% endtabs %}



## Get Collection Information

_<mark style="color:blue;">Included in: Basic, Pro, Dedicated</mark>_

<mark style="color:blue;">`GET`</mark> `https://api.bestinslot.xyz/v3/collection/info`

Returns detailed information about a specific collection.

Sample query: https://api.bestinslot.xyz/v3/collection/info?slug=degods

<mark style="color:orange;">**NOTE:**</mark> <mark style="color:orange;"></mark><mark style="color:orange;">inscription\_icon\_id may be a link for some collections</mark>

#### Query Parameters

| Name                                   | Type   | Description     |
| -------------------------------------- | ------ | --------------- |
| slug<mark style="color:red;">\*</mark> | string | Collection slug |

{% tabs %}
{% tab title="200: OK Success" %}
```json
{
    "data": {
        "name": "Strokes by zond",
        "twitter_link": "https://twitter.com/imgdotart",
        "discord_link": "https://discord.gg/nzQvtTfGJY",
        "website_link": "",
        "description": "",
        "supply": "16",
        "inscription_icon_id": "facd59ddb3d1822b6433eb297a1c4e11d46b75bb98559e3167f4f12e367da28ei0",
        "min_number": 131639,
        "median_number": 131647,
        "max_number": 131654,
        "icon_url": "https://bis-ord-content.fra1.cdn.digitaloceanspaces.com/ordinals/facd59ddb3d1822b6433eb297a1c4e11d46b75bb98559e3167f4f12e367da28ei0",
        "icon_render_url": "https://bis-ord-renders.fra1.cdn.digitaloceanspaces.com/renders/facd59ddb3d1822b6433eb297a1c4e11d46b75bb98559e3167f4f12e367da28ei0.png",
        "bis_url": "https://bestinslot.xyz/ordinals/collection/strokes-by-zond"
    },
    "block_height": 836797
}
```
{% endtab %}

{% tab title="429: Too Many Requests Rate limit exceeded" %}

{% endtab %}
{% endtabs %}



## Get Collection Holders

_<mark style="color:blue;">Included in: Basic, Pro, Dedicated</mark>_

<mark style="color:blue;">`GET`</mark> `https://api.bestinslot.xyz/v3/collection/holders`

Returns an array with holder information. Each entry has a wallet address and collected inscription ids.

Sample query: https://api.bestinslot.xyz/v3/collection/holders?slug=degods\
https://api.bestinslot.xyz/v3/collection/holders?slug=degods\&sort\_by=wallet\_addr\&order=asc\&offset=0\&count=100

#### Query Parameters

| Name                                   | Type   | Description                   |
| -------------------------------------- | ------ | ----------------------------- |
| slug<mark style="color:red;">\*</mark> | string | Collection slug               |
| sort\_by                               | string | (optional) "wallet\_addr"     |
| order                                  | string | (optional) "asc", "desc"      |
| offset                                 | int    | (optional) 0 <= offset        |
| count                                  | int    | (optional) 20 <= count <= 100 |

{% tabs %}
{% tab title="200: OK Success" %}
```json
{
    "data": [
        {
            "wallet": "bc1phw8w74ghl05k2h8lfxsmf45cygw4h6jhl7etm8qn5jjctpgyaxusl94w8s",
            "inscription_ids": [
                "22c8afa20c013499e278318e30e4745fbaa7b613e8b9a954d6d3661322c66816i0",
                "48c922a1d013c7d179c291f39dd0f2b3bc2c194a0bc464fdd16f52f11da4ad1ei0",
                "c8548df15991a6bd2dfb89cc421f0d4256cebf197768ec4c8183276e125237fbi0",
                "885c64b7d183330186cb20cd4bfeba4209e8f3c17939a0188634ddd7ebe34455i0",
                "2a285972320858c90c7ae2477c55ec106f9cc50caa9a4fa6d456cbfbaf2fac6di0",
                "faacc3092fd920711515f40997ea273a4c08967d6d2e7404ab73e2064d2ccd88i0"
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



## Get Collection Inscriptions

_<mark style="color:blue;">Included in: Basic, Pro, Dedicated</mark>_

<mark style="color:blue;">`GET`</mark> `https://api.bestinslot.xyz/v3/collection/inscriptions`

Returns ordered list of inscriptions of a specific collection.

Sample query: https://api.bestinslot.xyz/v3/collection/inscriptions?slug=bitcoin-frogs\&sort\_by=inscr\_num\&order=asc\&offset=100\&count=100

<mark style="color:orange;">**NOTE:**</mark> <mark style="color:orange;"></mark><mark style="color:orange;">last\_sale\_price is only available on Pro Tier.</mark>

#### Query Parameters

| Name                                       | Type   | Description        |
| ------------------------------------------ | ------ | ------------------ |
| sort\_by<mark style="color:red;">\*</mark> | string | inscr\_num         |
| order<mark style="color:red;">\*</mark>    | string | asc, desc          |
| offset<mark style="color:red;">\*</mark>   | int    | 0 <= offset        |
| count<mark style="color:red;">\*</mark>    | int    | 20 <= count <= 100 |
| slug<mark style="color:red;">\*</mark>     | string | collection slug    |

{% tabs %}
{% tab title="200: OK Success" %}
```json
{
    "data": [
        {
            "name": "Runestone",
            "inscription_id": "5f3dafcdd142358b332e0939d37174b76472735df8df29325901d2c7d18a152ci19",
            "inscription_number": 64362443,
            "metadata": {
                "name": "Runestone"
            },
            "owner_wallet_addr": "12dSsr8sFs21kpWaD2spSweFmyNzkZ8eRu",
            "mime_type": "model/gltf+json",
            "last_transfer_block_height": 834708,
            "parent_ids": [
                "fdb2df5d2b16db1ebcbf09e2d23b3f4e417db44b58e712c99b61f26b52c7cbb5i0"
            ],
            "genesis_height": 834708,
            "last_sale_price": null,
            "content_url": "https://bis-ord-content.fra1.cdn.digitaloceanspaces.com/ordinals/5f3dafcdd142358b332e0939d37174b76472735df8df29325901d2c7d18a152ci19",
            "bis_url": "https://bestinslot.xyz/ordinals/inscription/5f3dafcdd142358b332e0939d37174b76472735df8df29325901d2c7d18a152ci19",
            "render_url": null,
            "delegate": {
                "delegate_id": "ed76bf35918948b8b78be0e6397ad4916d926dd3d65679a8b7e67d8699a672a0i0",
                "render_url": "https://bis-ord-renders.fra1.cdn.digitaloceanspaces.com/renders/ed76bf35918948b8b78be0e6397ad4916d926dd3d65679a8b7e67d8699a672a0i0.png",
                "mime_type": "model/gltf+json",
                "content_url": "https://bis-ord-content.fra1.cdn.digitaloceanspaces.com/ordinals/ed76bf35918948b8b78be0e6397ad4916d926dd3d65679a8b7e67d8699a672a0i0",
                "bis_url": "https://bestinslot.xyz/ordinals/inscription/ed76bf35918948b8b78be0e6397ad4916d926dd3d65679a8b7e67d8699a672a0i0"
            }
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



## Get Collection Sales Information

_<mark style="color:blue;">Included in: Pro, Dedicated</mark>_

<mark style="color:blue;">`GET`</mark> `https://api.bestinslot.xyz/v3/collection/sales_info`

Returns sales and volume information about a specific collection.

Sample query: https://api.bestinslot.xyz/v3/collection/sales\_info?slug=bitcoin-frogs\&marketplace\_type=magiceden

#### Query Parameters

| Name                                   | Type   | Description                                                                                                 |
| -------------------------------------- | ------ | ----------------------------------------------------------------------------------------------------------- |
| slug<mark style="color:red;">\*</mark> | string | Collection slug                                                                                             |
| marketplace\_type                      | string | Optional parameter to filter only by a given marketplace. You can find the allowed types on Constants Page. |

{% tabs %}
{% tab title="200: OK Success" %}
```json
{
    "data": {
        "vol_3h": "9970000",
        "vol_6h": "45228879",
        "vol_9h": "82738348",
        "vol_12h": "94525896",
        "vol_1d": "140485613",
        "vol_3d": "995189800",
        "vol_7d": "2282078504",
        "vol_30d": "20435090360",
        "vol_total": "49541749144",
        "sale_count": 12274,
        "marketplace": "all"
    },
    "block_height": 795035
}
```
{% endtab %}

{% tab title="429: Too Many Requests Rate limit exceeded" %}

{% endtab %}

{% tab title="403: Forbidden Invalid API-Key" %}

{% endtab %}
{% endtabs %}



## Get Collection Market Information

_<mark style="color:blue;">Included in: Pro, Dedicated</mark>_

<mark style="color:blue;">`GET`</mark> `https://api.bestinslot.xyz/v3/collection/market_info`

Returns market information like marketcap, listed count, floor price about a specific collection.

Sample query: https://api.bestinslot.xyz/v3/collection/market\_info?slug=omb

#### Query Parameters

| Name                                   | Type   | Description     |
| -------------------------------------- | ------ | --------------- |
| slug<mark style="color:red;">\*</mark> | string | Collection slug |

{% tabs %}
{% tab title="200: OK Success" %}
```json
{
    "data": {
        "listed_count": 311,
        "floor_price": 20706000,
        "floor_price_ordswap": null,
        "floor_price_magiceden": 20706000,
        "floor_price_ordinalswallet": 300000000,
        "floor_price_gammaio": null,
        "floor_price_unisat": 100500000,
        "floor_price_ordynals": null,
        "floor_price_ordinalsmarket": null,
        "floor_price_okx": 57899999,
        "supply": "5243",
        "marketcap": 108561558000
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



## Get Collection Listings

_<mark style="color:blue;">Included in: Pro, Dedicated</mark>_

<mark style="color:blue;">`GET`</mark> `https://api.bestinslot.xyz/v3/collection/listings`

Returns ordered list of listings of a specific collection.

Sample query: https://api.bestinslot.xyz/v3/collection/listings?slug=bitcoin-frogs\&sort\_by=min\_price\&order=asc\&offset=0\&count=100

#### Query Parameters

| Name                                       | Type   | Description                                                                                                                                           |
| ------------------------------------------ | ------ | ----------------------------------------------------------------------------------------------------------------------------------------------------- |
| sort\_by<mark style="color:red;">\*</mark> | string | min\_price, ordswap\_price, magiceden\_price, ordinalswallet\_price, gammaio\_price, odynals\_price, unisat\_price, ordinalsmarket\_price, okx\_price |
| order<mark style="color:red;">\*</mark>    | string | asc, desc                                                                                                                                             |
| offset<mark style="color:red;">\*</mark>   | int    | 0 <= offset <= 5k                                                                                                                                     |
| count<mark style="color:red;">\*</mark>    | int    | 20 <= count <= 100                                                                                                                                    |
| slug<mark style="color:red;">\*</mark>     | string | collection slug                                                                                                                                       |

{% tabs %}
{% tab title="200: OK Success" %}
```json
{
    "data": [
        {
            "inscription_id": "02696786f173f05e55b457d12ef41bfcc905acd6ee5c0c61b80d8679a4ea91c9i0",
            "min_price": 4284000,
            "ordswap_price": null,
            "magiceden_price": 4284000,
            "ordinalswallet_price": null,
            "gammaio_price": null,
            "nostr_price": null,
            "odynals_price": null,
            "unisat_price": null,
            "ordinalsmarket_price": null,
            "okx_price": null,
            "owner_wallet_addr": "bc1pg95hedhcnrv9gu595n7ysy4apu6c0cz9vrs08dxd59p7kn5zyv0s6zdv0p"
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



## Get Collection Activity

_<mark style="color:blue;">Included in: Pro, Dedicated</mark>_

<mark style="color:blue;">`GET`</mark> `https://api.bestinslot.xyz/v3/collection/activity`

Returns ordered list of inscribes, sales and transfers of a specific collection.

<mark style="color:orange;">NOTE: Use last\_new\_satpoint to continue fetching the activity from where you've left off. new\_satpoint uniquely addresses a single inscription transfer, so by setting order to asc, and last\_new\_satpoint to the latest new\_satpoint value that you've received, you can retrieve the new activities.</mark>

Sample query: https://api.bestinslot.xyz/v3/collection/activity?slug=degods\&activity\_filter=7\&sort\_by=ts\&order=asc\&offset=0\&count=100\&last\_new\_satpoint=32b63c4844db4f704a8df0cf27fcf6ee966a716ea5410e598fe40734b1a7027f:1:0

#### Query Parameters

| Name                                               | Type   | Description                                                                                                                  |
| -------------------------------------------------- | ------ | ---------------------------------------------------------------------------------------------------------------------------- |
| sort\_by<mark style="color:red;">\*</mark>         | string | ts                                                                                                                           |
| order<mark style="color:red;">\*</mark>            | string | asc, desc                                                                                                                    |
| offset<mark style="color:red;">\*</mark>           | int    | 0 <= offset <= 5k                                                                                                            |
| count<mark style="color:red;">\*</mark>            | int    | 20 <= count <= 100                                                                                                           |
| slug<mark style="color:red;">\*</mark>             | string | collection slug                                                                                                              |
| activity\_filter<mark style="color:red;">\*</mark> | int    | <p>1 -> inscribed<br>2 -> transferred<br>4 -> sold<br>combine with or operator (e.g. sold &#x26; transferred: 2 | 4 = 6)</p> |
| last\_new\_satpoint                                | string | (optional) use this with offset 0 to continue from a known transfer                                                          |

{% tabs %}
{% tab title="200: OK Success" %}
```json
{
    "data": [
        {
            "inscription_id": "daf55547be8fd88f242ce24b3af11ec9f4d602b0c05b4b23967dfcd160ac719di0",
            "from_wallet": "bc1pm2grfjnvhrfjff965cs63gma5ze02v3572wks9mdl7kxjyt2q58q5es97l",
            "to_wallet": "bc1pdly22tta7wx56j9xhygzg5dwnd4a3xnj7qyt9ewrajn9hvmha9msfpm3sd",
            "block_height": 795034,
            "sale_price": -1,
            "new_satpoint": "5cd78b9bf19d80a1d525564ef7df775b65f0cc15e5f7bbafcb724c1b8995615c:0:0",
            "ts": "2023-06-19T09:30:18.000Z",
            "marketplace_type": "magiceden",
            "tx_id": "5cd78b9bf19d80a1d525564ef7df775b65f0cc15e5f7bbafcb724c1b8995615c"
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

