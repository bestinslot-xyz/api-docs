---
description: Endpoints related to sats names.
---

# Sats Names

Endpoints' API-Key-Tier availabilities are written for each endpoint.

**To use on testnet4/signet, use your current api-key and send the request to `https://testnet.api.bestinslot.xyz` / `https://signet_api.bestinslot.xyz`**

## Sats Validity Check

_<mark style="color:blue;">Included in: Basic, Pro, Dedicated</mark>_

<mark style="color:blue;">`GET`</mark> `https://api.bestinslot.xyz/v3/sats/validity_check`

Returns validity details about a specific inscription.

Sample query: https://api.bestinslot.xyz/v3/sats/validity\_check?inscription\_id=8ca50ea8ed42bf9b1b2dad8df4fddb1d354769b32d240e2d5a788ee78ef2bab0i0

#### Query Parameters

| Name                                              | Type   | Description    |
| ------------------------------------------------- | ------ | -------------- |
| inscription\_id<mark style="color:red;">\*</mark> | string | inscription id |

{% tabs %}
{% tab title="200: OK Success" %}
```json
{
    "data": {
        "sats_name": "penguins.sats",
        "original_id": "b8cd5daeb8859410c4cc01d88bfa5afe6c508713882af7099b45b5d583c270d7i0",
        "is_valid": false
    },
    "block_height": 795034
}
```
{% endtab %}

{% tab title="429: Too Many Requests Rate limit exceeded" %}

{% endtab %}
{% endtabs %}



## Sats Forward Lookup

_<mark style="color:blue;">Included in: Basic, Pro, Dedicated</mark>_

<mark style="color:blue;">`GET`</mark> `https://api.bestinslot.xyz/v3/sats/forward_lookup`

Returns address from a sats name.

Sample query: https://api.bestinslot.xyz/v3/sats/forward\_lookup?sats\_name=penguins.sats

#### Query Parameters

| Name                                         | Type   | Description |
| -------------------------------------------- | ------ | ----------- |
| sats\_name<mark style="color:red;">\*</mark> | string | sats name   |

{% tabs %}
{% tab title="200: OK Success" %}
```json
{
    "data": {
        "wallet": "bc1prjglj0tcff20fe4rkwlfj6rjpgjgp3c9k252gsrwysmc7uuk9dcqm40l8k",
        "bis_url": "https://bestinslot.xyz/bc1prjglj0tcff20fe4rkwlfj6rjpgjgp3c9k252gsrwysmc7uuk9dcqm40l8k"
    },
    "block_height": 795034
}
```
{% endtab %}

{% tab title="429: Too Many Requests Rate limit exceeded" %}

{% endtab %}
{% endtabs %}



## Sats Reverse Lookup

_<mark style="color:blue;">Included in: Basic, Pro, Dedicated</mark>_

<mark style="color:blue;">`GET`</mark> `https://api.bestinslot.xyz/v3/sats/reverse_lookup`

Returns valid sats name with minimum inscription number from a bitcoin wallet address.

Sample query: https://api.bestinslot.xyz/v3/sats/reverse\_lookup?address=bc1prjglj0tcff20fe4rkwlfj6rjpgjgp3c9k252gsrwysmc7uuk9dcqm40l8k

#### Query Parameters

| Name                                      | Type   | Description            |
| ----------------------------------------- | ------ | ---------------------- |
| address<mark style="color:red;">\*</mark> | string | bitcoin wallet address |

{% tabs %}
{% tab title="200: OK Success" %}
```json
{
    "data": {
        "name": "cindi.sats",
        "bis_url": "https://bestinslot.xyz/cindi.sats"
    },
    "block_height": 795034
}
```
{% endtab %}

{% tab title="429: Too Many Requests Rate limit exceeded" %}

{% endtab %}
{% endtabs %}



## Get Sats Activity

_<mark style="color:blue;">Included in: Pro, Dedicated</mark>_

<mark style="color:blue;">`GET`</mark> `https://api.bestinslot.xyz/v3/sats/activity`

Returns ordered list of inscribes, sales and transfers of all sats.

Sample query: https://api.bestinslot.xyz/v3/sats/activity?activity\_filter=7\&sort\_by=ts\&order=desc\&offset=0\&count=100

#### Query Parameters

| Name                                               | Type   | Description                                                                                                                  |
| -------------------------------------------------- | ------ | ---------------------------------------------------------------------------------------------------------------------------- |
| sort\_by<mark style="color:red;">\*</mark>         | string | ts                                                                                                                           |
| order<mark style="color:red;">\*</mark>            | string | asc, desc                                                                                                                    |
| offset<mark style="color:red;">\*</mark>           | int    | 0 <= offset <= 5k                                                                                                            |
| count<mark style="color:red;">\*</mark>            | int    | 20 <= count <= 100                                                                                                           |
| activity\_filter<mark style="color:red;">\*</mark> | int    | <p>1 -> inscribed<br>2 -> transferred<br>4 -> sold<br>combine with or operator (e.g. sold &#x26; transferred: 2 | 4 = 6)</p> |

{% tabs %}
{% tab title="200: OK Success" %}
```json
{
    "data": [
        {
            "inscription_id": "04a5e6e80d49eae28b6da1185eae2566acf438f52957ca214a262ff1a398d469i0",
            "from_wallet": "bc1qzfcrcx5xtsc25dkzls9smmr45fztfpwyznnmzh",
            "to_wallet": "bc1pnvfmyadyqy6ggdhqaktm7crs3tgpnvadc9rnt973axfr6twend6qexd5qz",
            "block_height": 801580,
            "sale_price": 3531,
            "new_satpoint": "a54d450288ae6ea1165ea02ac3e60b69d56b172ea9fb77ab2011b15cbeb6eeb3:1:0",
            "ts": "2023-08-04T01:10:16.000Z",
            "marketplace_type": "magiceden",
            "tx_id": "a54d450288ae6ea1165ea02ac3e60b69d56b172ea9fb77ab2011b15cbeb6eeb3"
        },
        ...
    ],
    "block_height": 801585
}
```
{% endtab %}

{% tab title="429: Too Many Requests Rate limit exceeded" %}

{% endtab %}

{% tab title="403: Forbidden Invalid API-Key" %}

{% endtab %}
{% endtabs %}
