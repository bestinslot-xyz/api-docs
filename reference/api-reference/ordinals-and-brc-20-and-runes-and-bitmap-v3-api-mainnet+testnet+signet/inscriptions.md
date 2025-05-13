---
description: Endpoints related to Inscription Details.
---

# Inscriptions

Endpoints' API-Key-Tier availabilities are written for each endpoint.

**To use on testnet4/signet, use your current api-key and send the request to `https://testnet.api.bestinslot.xyz` / `https://signet_api.bestinslot.xyz`**

## Get Inscription Information

_<mark style="color:blue;">Included in: Basic, Pro, Dedicated</mark>_

<mark style="color:blue;">`GET`</mark> `https://api.bestinslot.xyz/v3/inscription/single_info_id`

Returns detailed information about a specific inscription.

Sample query: https://api.bestinslot.xyz/v3/inscription/single\_info\_id?inscription\_id=6d1cefe69ad686d6153bd1a6d34c6d55c6e3162cb2fac9b58a8d9d9e9fda13c6i0

<mark style="color:orange;">**NOTE:**</mark> <mark style="color:orange;"></mark><mark style="color:orange;">last\_sale\_price, listing prices and collection\_floor\_price is only available on Pro Tier.</mark>

#### Query Parameters

| Name                                              | Type   | Description    |
| ------------------------------------------------- | ------ | -------------- |
| inscription\_id<mark style="color:red;">\*</mark> | string | inscription id |

{% tabs %}
{% tab title="200: OK Success" %}
```json
{
    "data": {
        "inscription_name": "Runestone",
        "inscription_id": "5f3dafcdd142358b332e0939d37174b76472735df8df29325901d2c7d18a152ci19",
        "inscription_number": 64362443,
        "metadata": {
            "name": "Runestone"
        },
        "wallet": "12dSsr8sFs21kpWaD2spSweFmyNzkZ8eRu",
        "mime_type": "model/gltf+json",
        "media_length": 0,
        "genesis_ts": 1710447063,
        "genesis_height": 834708,
        "genesis_fee": 1345,
        "output_value": 546,
        "satpoint": "5f3dafcdd142358b332e0939d37174b76472735df8df29325901d2c7d18a152c:20:0",
        "last_sale_price": null,
        "collection_name": "Runestone",
        "collection_slug": "runestone",
        "last_transfer_block_height": 834708,
        "utxo": "5f3dafcdd142358b332e0939d37174b76472735df8df29325901d2c7d18a152c:20",
        "parent_ids": [
            "fdb2df5d2b16db1ebcbf09e2d23b3f4e417db44b58e712c99b61f26b52c7cbb5i0"
        ],
        "collection_floor_price": 3950000,
        "min_price": null,
        "ordswap_price": null,
        "magiceden_price": null,
        "ordinalswallet_price": null,
        "gammaio_price": null,
        "nostr_price": null,
        "odynals_price": null,
        "unisat_price": null,
        "ordinalsmarket_price": null,
        "okx_price": null,
        "content_url": "https://bis-ord-content.fra1.cdn.digitaloceanspaces.com/ordinals/5f3dafcdd142358b332e0939d37174b76472735df8df29325901d2c7d18a152ci19",
        "bis_url": "https://bestinslot.xyz/ordinals/inscription/5f3dafcdd142358b332e0939d37174b76472735df8df29325901d2c7d18a152ci19",
        "render_url": null,
        "byte_size": 0,
        "bitmap_number": null,
        "delegate": {
            "delegate_id": "ed76bf35918948b8b78be0e6397ad4916d926dd3d65679a8b7e67d8699a672a0i0",
            "render_url": "https://bis-ord-renders.fra1.cdn.digitaloceanspaces.com/renders/ed76bf35918948b8b78be0e6397ad4916d926dd3d65679a8b7e67d8699a672a0i0.png",
            "mime_type": "model/gltf+json",
            "content_url": "https://bis-ord-content.fra1.cdn.digitaloceanspaces.com/ordinals/ed76bf35918948b8b78be0e6397ad4916d926dd3d65679a8b7e67d8699a672a0i0",
            "bis_url": "https://bestinslot.xyz/ordinals/inscription/ed76bf35918948b8b78be0e6397ad4916d926dd3d65679a8b7e67d8699a672a0i0"
        }
    },
    "block_height": 836798
}
```
{% endtab %}

{% tab title="429: Too Many Requests Rate limit exceeded" %}

{% endtab %}
{% endtabs %}



## Get Batch Inscription Information

_<mark style="color:blue;">Included in: Basic, Pro, Dedicated</mark>_

<mark style="color:green;">`POST`</mark> `https://api.bestinslot.xyz/v3/inscription/batch_info`

Returns detailed information about several inscriptions (up to 100).

Sample query:\
url: https://api.bestinslot.xyz/v3/inscription/batch\_info\
data: {"queries":\["0", 1, "123", 17458374, -123, 32478238472934]}\
headers: { "Content-Type":"application/json", "x-api-key":"...." }

<mark style="color:orange;">**NOTE:**</mark> <mark style="color:orange;"></mark><mark style="color:orange;">last\_sale\_price, listing prices and collection\_floor\_price is only available on Pro Tier.</mark>

#### Request Body

| Name                                      | Type       | Description                                                                                                                          |
| ----------------------------------------- | ---------- | ------------------------------------------------------------------------------------------------------------------------------------ |
| queries<mark style="color:red;">\*</mark> | JSON Array | can be a list of inscription id, inscription number or location (txid:index), however all types must be the same. Max length is 100. |

{% tabs %}
{% tab title="200: OK Success" %}
```json
{
    "data": [
        {
            "query": "5f3dafcdd142358b332e0939d37174b76472735df8df29325901d2c7d18a152ci1",
            "result": {
                "inscription_name": "Runestone",
                "inscription_id": "5f3dafcdd142358b332e0939d37174b76472735df8df29325901d2c7d18a152ci1",
                "inscription_number": 64362425,
                "metadata": {
                    "name": "Runestone"
                },
                "wallet": "113zRn6gi97iAriKbXTFtkgqSeVmAD32uA",
                "mime_type": "model/gltf+json",
                "media_length": 0,
                "genesis_ts": 1710447063,
                "genesis_height": 834708,
                "genesis_fee": 1345,
                "output_value": 546,
                "satpoint": "5f3dafcdd142358b332e0939d37174b76472735df8df29325901d2c7d18a152c:2:0",
                "last_sale_price": null,
                "collection_name": "Runestone",
                "collection_slug": "runestone",
                "last_transfer_block_height": 834708,
                "utxo": "5f3dafcdd142358b332e0939d37174b76472735df8df29325901d2c7d18a152c:2",
                "parent_ids": [
                    "fdb2df5d2b16db1ebcbf09e2d23b3f4e417db44b58e712c99b61f26b52c7cbb5i0"
                ],
                "genesis_block_hash": "00000000000000000000292964b4b00d1d414583bd18d1ebea7a8041d4409c6d",
                "collection_floor_price": 3950000,
                "min_price": null,
                "ordswap_price": null,
                "magiceden_price": null,
                "ordinalswallet_price": null,
                "gammaio_price": null,
                "nostr_price": null,
                "odynals_price": null,
                "unisat_price": null,
                "ordinalsmarket_price": null,
                "okx_price": null,
                "content_url": "https://bis-ord-content.fra1.cdn.digitaloceanspaces.com/ordinals/5f3dafcdd142358b332e0939d37174b76472735df8df29325901d2c7d18a152ci1",
                "bis_url": "https://bestinslot.xyz/ordinals/inscription/5f3dafcdd142358b332e0939d37174b76472735df8df29325901d2c7d18a152ci1",
                "render_url": null,
                "byte_size": 0,
                "bitmap_number": null,
                "delegate": {
                    "delegate_id": "ed76bf35918948b8b78be0e6397ad4916d926dd3d65679a8b7e67d8699a672a0i0",
                    "render_url": "https://bis-ord-renders.fra1.cdn.digitaloceanspaces.com/renders/ed76bf35918948b8b78be0e6397ad4916d926dd3d65679a8b7e67d8699a672a0i0.png",
                    "mime_type": "model/gltf+json",
                    "content_url": "https://bis-ord-content.fra1.cdn.digitaloceanspaces.com/ordinals/ed76bf35918948b8b78be0e6397ad4916d926dd3d65679a8b7e67d8699a672a0i0",
                    "bis_url": "https://bestinslot.xyz/ordinals/inscription/ed76bf35918948b8b78be0e6397ad4916d926dd3d65679a8b7e67d8699a672a0i0"
                }
            }
        },
        ...
    ],
    "block_height": 804350
}
```
{% endtab %}

{% tab title="429: Too Many Requests Rate limit exceeded" %}

{% endtab %}
{% endtabs %}



## Get Global Inscription Information

_<mark style="color:blue;">Included in: Basic, Pro, Dedicated</mark>_

<mark style="color:blue;">`GET`</mark> `https://api.bestinslot.xyz/v3/inscription/global_info`

Returns information about global inscriptions.

Sample query: https://api.bestinslot.xyz/v3/inscription/global\_info

{% tabs %}
{% tab title="200: OK Success" %}
```json
{
    "data": [
        {
            "text_cnt": 24513963,
            "image_cnt": 1118329,
            "application_cnt": 299961,
            "video_cnt": 1932,
            "model_cnt": 469,
            "audio_cnt": 666,
            "max_inscription_number": 25935380
        }
    ],
    "block_height": 804350
}
```
{% endtab %}

{% tab title="429: Too Many Requests Rate limit exceeded" %}

{% endtab %}
{% endtabs %}



## Request render refresh

_<mark style="color:blue;">Included in: Basic, Pro, Dedicated</mark>_

<mark style="color:blue;">`GET`</mark> `https://api.bestinslot.xyz/v3/inscription/render_refresh`

Requests render refresh for given inscription.

Sample query: https://api.bestinslot.xyz/v3/inscription/render\_refresh?inscription\_id=8e9cdfb606db7abd839fdbc5eb1678ee60c9d6b1b008790ed1052ddadac12877i71

<mark style="color:orange;">**NOTE:**</mark> returns `already-in-queue` or `added-to-queue`.

#### Query Parameters

| Name                                              | Type   | Description    |
| ------------------------------------------------- | ------ | -------------- |
| inscription\_id<mark style="color:red;">\*</mark> | string | inscription id |

{% tabs %}
{% tab title="200: OK Success" %}
```json
{
    "data": "added-to-queue",
    "block_height": 889397
}
```
{% endtab %}

{% tab title="429: Too Many Requests Rate limit exceeded" %}

{% endtab %}
{% endtabs %}



## Get Inscription Activity

_<mark style="color:blue;">Included in: Pro, Dedicated</mark>_

<mark style="color:blue;">`GET`</mark> `https://api.bestinslot.xyz/v3/inscription/activity`

Returns ordered list of inscribes, sales and transfers of a single inscription.

Sample query: https://api.bestinslot.xyz/v3/inscription/activity?inscription\_id=2f1d51c67998d981055e94dba30d3d1199aa9714049801d7cd35c72066c586abi0\&activity\_filter=7\&sort\_by=ts\&order=desc\&offset=0\&count=100

#### Query Parameters

| Name                                               | Type   | Description                                                                                                                  |
| -------------------------------------------------- | ------ | ---------------------------------------------------------------------------------------------------------------------------- |
| sort\_by<mark style="color:red;">\*</mark>         | string | ts                                                                                                                           |
| order<mark style="color:red;">\*</mark>            | string | asc, desc                                                                                                                    |
| offset<mark style="color:red;">\*</mark>           | int    | 0 <= offset <= 5k                                                                                                            |
| count<mark style="color:red;">\*</mark>            | int    | 20 <= count <= 100                                                                                                           |
| inscription\_id<mark style="color:red;">\*</mark>  | string | inscription id                                                                                                               |
| activity\_filter<mark style="color:red;">\*</mark> | int    | <p>1 -> inscribed<br>2 -> transferred<br>4 -> sold<br>combine with or operator (e.g. sold &#x26; transferred: 2 | 4 = 6)</p> |

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



## Get Inscriptions in Transaction

_<mark style="color:blue;">Included in: Basic, Pro, Dedicated</mark>_

<mark style="color:blue;">`GET`</mark> `https://api.bestinslot.xyz/v3/inscription/in_transaction`

Returns inscription ids that move in a given transaction.

Sample query: https://api.bestinslot.xyz/v3/inscription/in\_transaction?tx\_id=5c709dbe85c44935384a3d68d10f9212b1ee315bba422cb8b5944803b521a3db

#### Query Parameters

| Name                                     | Type   | Description            |
| ---------------------------------------- | ------ | ---------------------- |
| tx\_id<mark style="color:red;">\*</mark> | string | Bitcoin Transaction Id |

{% tabs %}
{% tab title="200: OK Success" %}
```json
{
    "data": [
        {
            "inscription_id": "7fd3aca38fd8acb22efe231ef5d5439e391c0394be3967ee07484cffc1b792fai0"
        },
        {
            "inscription_id": "251c744ceb0ad4c6e1ee0d391cfa0451d958065e73605b543190cda62723f6f8i0"
        },
        {
            "inscription_id": "b089b8df8392d0ac3b47b8e51fb008aa40442b6bb250ad2a1d8d60d88cc65585i0"
        },
        {
            "inscription_id": "ec9570ada981607bd93a5a7e6fd99760faaa8fc87989aa6646fe8c9b2aab494ei0"
        },
        {
            "inscription_id": "7c679ba4a2b8460fb60d62912e812206a031abeef19983564953c14bb4e091d5i0"
        },
        {
            "inscription_id": "9c233d4b62e1fde06c1a238fcef26e398eaee5a9abf32a6de8eef12cd4e523dai0"
        }
    ],
    "block_height": 815901
}
```
{% endtab %}

{% tab title="429: Too Many Requests Rate limit exceeded" %}

{% endtab %}
{% endtabs %}



## Get Inscription Activity in Block

_<mark style="color:blue;">Included in: Enterprise, Dedicated with Enterprise Endpoints</mark>_

<mark style="color:blue;">`GET`</mark> `https://api.bestinslot.xyz/v3/inscription/activity_on_block`

Returns the inscription activity on a given block\_height

<mark style="color:orange;">NOTE: block\_height at the response is not the queried block height. It is the final indexed block height of our indexer.</mark>

Sample query: \
https://api.bestinslot.xyz/v3/inscription/activity\_on\_block?block\_height=802397

https://api.bestinslot.xyz/v3/inscription/activity\_on\_block?block\_height=802397\&sort\_by=ts\&order=asc\&activity\_filter=4

#### Query Parameters

| Name                                            | Type   | Description                                                                                                                  |
| ----------------------------------------------- | ------ | ---------------------------------------------------------------------------------------------------------------------------- |
| block\_height<mark style="color:red;">\*</mark> | int    | block height, must not be bigger than current bitcoin block height                                                           |
| order                                           | string | asc, desc                                                                                                                    |
| sort\_by                                        | string | ts                                                                                                                           |
| activity\_filter                                | int    | <p>1 -> inscribed<br>2 -> transferred<br>4 -> sold<br>combine with or operator (e.g. sold &#x26; transferred: 2 | 4 = 6)</p> |

{% tabs %}
{% tab title="200: OK Success" %}
```json
{
    "data": [
        {
            "inscription_id": "b4f3838eecc0600531264e3dfcffbe997c73d77c7aa6fb7e9afc7cc20fad2fa9i0",
            "from_wallet": "bc1pz5sdw9zqek9vhc52w7du4yskwk8rmcz0m7wmqhfv24gv5tdqqzcqpwvdt0",
            "to_wallet": "bc1pk6t7u08vtpx7r79m8hhxrhsd9s7xpqck9aa75hlgq3fm8ww83n9s8hex94",
            "block_height": 805002,
            "sale_price": 417950,
            "new_satpoint": "fab1dbe521900e73a87b2410c84559320cbdf7b21415fbfc57a1d5dfbed662de:1:0",
            "ts": "2023-08-27T04:12:43.000Z",
            "marketplace_type": "magiceden",
            "inscription_name": "Ordinal Insider #29",
            "inscription_number": 921122,
            "collection_name": "Ordinal Insiders",
            "collection_slug": "ordinal-insiders",
            "tx_id": "fab1dbe521900e73a87b2410c84559320cbdf7b21415fbfc57a1d5dfbed662de"
        },
        ...
    ],
    "block_height": 815969
}
```
{% endtab %}

{% tab title="429: Too Many Requests Rate limit exceeded" %}

{% endtab %}

{% tab title="403: Forbidden Invalid API-Key" %}

{% endtab %}
{% endtabs %}



## Get New Inscriptions in Block

_<mark style="color:blue;">Included in: Enterprise, Dedicated with Enterprise Endpoints</mark>_

<mark style="color:blue;">`GET`</mark> `https://api.bestinslot.xyz/v3/inscription/new_inscriptions_in_block`

Returns the inscriptions that are inscribed in a given block\_height

<mark style="color:orange;">NOTE: block\_height at the response is not the queried block height. It is the final indexed block height of our indexer.</mark>

Sample query: https://api.bestinslot.xyz/v3/inscription/new\_inscriptions\_in\_block?block\_height=802397

#### Query Parameters

| Name                                            | Type | Description                                                        |
| ----------------------------------------------- | ---- | ------------------------------------------------------------------ |
| block\_height<mark style="color:red;">\*</mark> | int  | block height, must not be bigger than current bitcoin block height |

{% tabs %}
{% tab title="200: OK Success" %}
```json
{
    "data": [
        {
            "inscription_name": "Runestone",
            "inscription_id": "5f3dafcdd142358b332e0939d37174b76472735df8df29325901d2c7d18a152ci0",
            "inscription_number": 64362424,
            "metadata": {
                "name": "Runestone"
            },
            "wallet": "1111111111111111111114oLvT2",
            "mime_type": "model/gltf+json",
            "media_length": 0,
            "genesis_ts": 1710447063,
            "genesis_height": 834708,
            "genesis_fee": 1345,
            "output_value": 546,
            "satpoint": "5f3dafcdd142358b332e0939d37174b76472735df8df29325901d2c7d18a152c:1:0",
            "last_sale_price": null,
            "collection_name": "Runestone",
            "collection_slug": "runestone",
            "last_transfer_block_height": 834708,
            "parent_ids": [
                "fdb2df5d2b16db1ebcbf09e2d23b3f4e417db44b58e712c99b61f26b52c7cbb5i0"
            ],
            "collection_floor_price": 3950000,
            "min_price": null,
            "ordswap_price": null,
            "magiceden_price": null,
            "ordinalswallet_price": null,
            "gammaio_price": null,
            "nostr_price": null,
            "odynals_price": null,
            "unisat_price": null,
            "ordinalsmarket_price": null,
            "okx_price": null,
            "content_url": "https://bis-ord-content.fra1.cdn.digitaloceanspaces.com/ordinals/5f3dafcdd142358b332e0939d37174b76472735df8df29325901d2c7d18a152ci0",
            "bis_url": "https://bestinslot.xyz/ordinals/inscription/5f3dafcdd142358b332e0939d37174b76472735df8df29325901d2c7d18a152ci0",
            "render_url": null,
            "byte_size": 0,
            "bitmap_number": null,
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
    "block_height": 804496
}
```
{% endtab %}

{% tab title="429: Too Many Requests Rate limit exceeded" %}

{% endtab %}

{% tab title="403: Forbidden Invalid API-Key" %}

{% endtab %}
{% endtabs %}
