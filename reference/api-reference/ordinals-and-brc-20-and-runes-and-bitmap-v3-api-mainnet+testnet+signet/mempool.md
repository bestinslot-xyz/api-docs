---
description: Endpoints related to Bitcoin Mempool & UTXOs.
---

# Mempool

Endpoints' API-Key-Tier availabilities are written for each endpoint.

**To use on testnet4/signet, use your current api-key and send the request to `https://testnet.api.bestinslot.xyz` / `https://signet_api.bestinslot.xyz`**

## Get All UTXOs of Bitcoin Wallet

_<mark style="color:blue;">Included in: Pro, Dedicated</mark>_

<mark style="color:blue;">`GET`</mark> `https://api.bestinslot.xyz/v3/mempool/all_utxos_of_wallet`

Returns all UTXOs of a given wallet with inscription and runes information.

Sample query: https://api.bestinslot.xyz/v3/mempool/all\_utxos\_of\_wallet?wallet\_addr=bc1qvhl8k0xu0stk956tjqx6q5ujp6tdyh24v7eumn

<mark style="color:orange;">**NOTE: Unconfirmed UTXOs block\_height is returned as null**</mark>

#### Query Parameters

| Name                                           | Type     | Description            |
| ---------------------------------------------- | -------- | ---------------------- |
| wallet\_addr<mark style="color:red;">\*</mark> | `string` | Bitcoin wallet address |

{% tabs %}
{% tab title="200: OK Success" %}
```json
{
    "data": [
        {
            "txid": "f48fd528ecb4c32252a6b0ad4bcd07123ad0c583fb808f9bdd04a7c015c60446",
            "vout": 0,
            "block_height": 803100,
            "value": 9109,
            "address": "bc1qvhl8k0xu0stk956tjqx6q5ujp6tdyh24v7eumn",
            "script": "001465fe7b3cdc7c1762d34b900da053920e96d25d55",
            "script_type": "witness_v0_keyhash",
            "inscription_ids": [
                "b3521d61a5cfdb80c4957cf7e4ce6c7f3e263b8baba05c787f003f17cacef97bi0"
            ],
            "satpoints": [
                "f48fd528ecb4c32252a6b0ad4bcd07123ad0c583fb808f9bdd04a7c015c60446:0:0"
            ],
            "rune_ids": null,
            "amounts": null,
            "txfee": null,
            "vsize": null,
            "utxo": "f48fd528ecb4c32252a6b0ad4bcd07123ad0c583fb808f9bdd04a7c015c60446:0"
        },
        {
            "txid": "c04e49f6393a571b95f711038746ea78ba673e0a0a2a71be7daccefe6143b154",
            "vout": 1,
            "block_height": null,
            "value": 546,
            "address": "bc1qvhl8k0xu0stk956tjqx6q5ujp6tdyh24v7eumn",
            "script": "001465fe7b3cdc7c1762d34b900da053920e96d25d55",
            "script_type": "witness_v0_keyhash",
            "inscription_ids": null,
            "satpoints": null,
            "rune_ids": [
                "840000:3"
            ],
            "amounts": [
                "209286845"
            ],
            "txfee": "1274",
            "vsize": 253,
            "utxo": "c04e49f6393a571b95f711038746ea78ba673e0a0a2a71be7daccefe6143b154:1"
        },
        ...
    ],
    "block_height": 863641
}
```
{% endtab %}
{% endtabs %}



## Get Cardinal UTXOs of Bitcoin Wallet

_<mark style="color:blue;">Included in: Pro, Dedicated</mark>_

<mark style="color:blue;">`GET`</mark> `https://api.bestinslot.xyz/v3/mempool/cardinal_utxos_of_wallet`

Returns cardinal UTXOs of a given wallet.

Sample query: https://api.bestinslot.xyz/v3/mempool/cardinal\_utxos\_of\_wallet?wallet\_addr=bc1qvhl8k0xu0stk956tjqx6q5ujp6tdyh24v7eumn

<mark style="color:orange;">**NOTE: Unconfirmed UTXOs block\_height is returned as null**</mark>

#### Query Parameters

| Name                                           | Type     | Description            |
| ---------------------------------------------- | -------- | ---------------------- |
| wallet\_addr<mark style="color:red;">\*</mark> | `string` | Bitcoin wallet address |

{% tabs %}
{% tab title="200: OK Success" %}
```json
{
    "data": [
        {
            "txid": "c04e49f6393a571b95f711038746ea78ba673e0a0a2a71be7daccefe6143b154",
            "vout": 3,
            "block_height": 863642,
            "value": 61150,
            "address": "bc1qvhl8k0xu0stk956tjqx6q5ujp6tdyh24v7eumn",
            "script": "001465fe7b3cdc7c1762d34b900da053920e96d25d55",
            "script_type": "witness_v0_keyhash",
            "inscription_ids": null,
            "satpoints": null,
            "rune_ids": null,
            "amounts": null,
            "txfee": null,
            "vsize": null,
            "utxo": "c04e49f6393a571b95f711038746ea78ba673e0a0a2a71be7daccefe6143b154:3"
        },
        ...
    ],
    "block_height": 863642
}
```
{% endtab %}
{% endtabs %}



## Get Ordinal UTXOs of Bitcoin Wallet

_<mark style="color:blue;">Included in: Pro, Dedicated</mark>_

<mark style="color:blue;">`GET`</mark> `https://api.bestinslot.xyz/v3/mempool/ordinal_utxos_of_wallet`

Returns ordinal UTXOs of a given wallet with inscription.

Sample query: https://api.bestinslot.xyz/v3/mempool/ordinal\_utxos\_of\_wallet?wallet\_addr=bc1qvhl8k0xu0stk956tjqx6q5ujp6tdyh24v7eumn

<mark style="color:orange;">**NOTE: Unconfirmed UTXOs block\_height is returned as null**</mark>

#### Query Parameters

| Name                                           | Type     | Description            |
| ---------------------------------------------- | -------- | ---------------------- |
| wallet\_addr<mark style="color:red;">\*</mark> | `string` | Bitcoin wallet address |

{% tabs %}
{% tab title="200: OK Success" %}
```json
{
    "data": [
        {
            "txid": "f48fd528ecb4c32252a6b0ad4bcd07123ad0c583fb808f9bdd04a7c015c60446",
            "vout": 0,
            "block_height": 803100,
            "value": 9109,
            "address": "bc1qvhl8k0xu0stk956tjqx6q5ujp6tdyh24v7eumn",
            "script": "001465fe7b3cdc7c1762d34b900da053920e96d25d55",
            "script_type": "witness_v0_keyhash",
            "inscription_ids": [
                "b3521d61a5cfdb80c4957cf7e4ce6c7f3e263b8baba05c787f003f17cacef97bi0"
            ],
            "satpoints": [
                "f48fd528ecb4c32252a6b0ad4bcd07123ad0c583fb808f9bdd04a7c015c60446:0:0"
            ],
            "rune_ids": null,
            "amounts": null,
            "txfee": null,
            "vsize": null,
            "utxo": "f48fd528ecb4c32252a6b0ad4bcd07123ad0c583fb808f9bdd04a7c015c60446:0"
        },
        ...
    ],
    "block_height": 863642
}
```
{% endtab %}
{% endtabs %}



## Get Runic UTXOs of Bitcoin Wallet

_<mark style="color:blue;">Included in: Pro, Dedicated</mark>_

<mark style="color:blue;">`GET`</mark> `https://api.bestinslot.xyz/v3/mempool/runic_utxos_of_wallet`

Returns runic UTXOs of a given wallet with runes information.

Sample query: https://api.bestinslot.xyz/v3/mempool/runic\_utxos\_of\_wallet?wallet\_addr=bc1qvhl8k0xu0stk956tjqx6q5ujp6tdyh24v7eumn

<mark style="color:orange;">**NOTE: Unconfirmed UTXOs block\_height is returned as null**</mark>

#### Query Parameters

| Name                                           | Type     | Description            |
| ---------------------------------------------- | -------- | ---------------------- |
| wallet\_addr<mark style="color:red;">\*</mark> | `string` | Bitcoin wallet address |

{% tabs %}
{% tab title="200: OK Success" %}
```json
{
    "data": [
        {
            "txid": "c04e49f6393a571b95f711038746ea78ba673e0a0a2a71be7daccefe6143b154",
            "vout": 1,
            "block_height": 863642,
            "value": 546,
            "address": "bc1qvhl8k0xu0stk956tjqx6q5ujp6tdyh24v7eumn",
            "script": "001465fe7b3cdc7c1762d34b900da053920e96d25d55",
            "script_type": "witness_v0_keyhash",
            "inscription_ids": null,
            "satpoints": null,
            "rune_ids": [
                "840000:3"
            ],
            "amounts": [
                "209286845"
            ],
            "txfee": null,
            "vsize": null,
            "utxo": "c04e49f6393a571b95f711038746ea78ba673e0a0a2a71be7daccefe6143b154:1"
        },
        ...
    ],
    "block_height": 863642
}
```
{% endtab %}
{% endtabs %}



## Get Cardinal Balance of Bitcoin Wallet

_<mark style="color:blue;">Included in: Pro, Dedicated</mark>_

<mark style="color:blue;">`GET`</mark> `https://api.bestinslot.xyz/v3/mempool/cardinal_balance_of_wallet`

Returns cardinal balance of a given wallet.

Sample query: https://api.bestinslot.xyz/v3/mempool/cardinal\_balance\_of\_wallet?wallet\_addr=bc1qvhl8k0xu0stk956tjqx6q5ujp6tdyh24v7eumn

#### Query Parameters

| Name                                           | Type     | Description            |
| ---------------------------------------------- | -------- | ---------------------- |
| wallet\_addr<mark style="color:red;">\*</mark> | `string` | Bitcoin wallet address |

{% tabs %}
{% tab title="200: OK Success" %}
```json
{
    "data": {
        "total_unused_confirmed_balance": "61150",
        "total_unused_unconfirmed_balance": "0"
    },
    "block_height": 863642
}
```
{% endtab %}
{% endtabs %}



## Get All Cardinal UTXOs in Mempool

_<mark style="color:blue;">Included in: Dedicated</mark>_

<mark style="color:blue;">`GET`</mark> `https://api.bestinslot.xyz/v3/mempool/all_cardinal_utxos`

Returns all cardinal UTXOs in Mempool.

Sample query: https://api.bestinslot.xyz/v3/mempool/all\_cardinal\_utxos



{% tabs %}
{% tab title="200: OK Success" %}
```json
{
    "data": [
        {
            "txid": "2f8de7eb0b12a9517c2ac122f37bb51867ee9a78b0c27308f2c09628af8e207e",
            "vout": 0,
            "block_height": null,
            "value": 2522422,
            "address": "bc1q9xap3eck8tqdz3y86wzhf85xewr8a75slq88nj",
            "script": "001429ba18e7163ac0d14487d385749e86cb867efa90",
            "script_type": "witness_v0_keyhash",
            "inscription_ids": null,
            "satpoints": null,
            "rune_ids": null,
            "amounts": null,
            "txfee": "774",
            "vsize": 177,
            "utxo": "2f8de7eb0b12a9517c2ac122f37bb51867ee9a78b0c27308f2c09628af8e207e:0"
        },
        ...
    ],
    "block_height": 889388
}
```
{% endtab %}
{% endtabs %}



## Get All Ordinal UTXOs in Mempool

_<mark style="color:blue;">Included in: Dedicated</mark>_

<mark style="color:blue;">`GET`</mark> `https://api.bestinslot.xyz/v3/mempool/all_ordinal_utxos`

Returns all Ordinal UTXOs in Mempool.

Sample query: https://api.bestinslot.xyz/v3/mempool/all\_ordinal\_utxos

{% tabs %}
{% tab title="200: OK Success" %}
```json
{
    "data": [
        {
            "txid": "375e43025d156cf496563859f46e6d590d49b86f0df158671be290eaadb13287",
            "vout": 0,
            "block_height": null,
            "value": 330,
            "address": "bc1pxmahywzrmzlrjndrg3ele2whalmv70elnzdq0ml2nvmhfc5k039snhqpt7",
            "script": "512036fb723843d8be394da34473fca9d7eff6cf3f3f989a07efea9b3774e2967c4b",
            "script_type": "witness_v1_taproot",
            "inscription_ids": [
                "375e43025d156cf496563859f46e6d590d49b86f0df158671be290eaadb13287i0"
            ],
            "satpoints": [
                "375e43025d156cf496563859f46e6d590d49b86f0df158671be290eaadb13287:0:0"
            ],
            "rune_ids": null,
            "amounts": null,
            "txfee": "158",
            "vsize": 151,
            "utxo": "375e43025d156cf496563859f46e6d590d49b86f0df158671be290eaadb13287:0"
        },
        ...
    ],
    "block_height": 889388
}
```
{% endtab %}
{% endtabs %}



## Get All Runic UTXOs in Mempool

_<mark style="color:blue;">Included in: Pro, Dedicated</mark>_

<mark style="color:blue;">`GET`</mark> `https://api.bestinslot.xyz/v3/mempool/all_runic_utxos`

Returns all Runic UTXOs in Mempool.

Sample query: https://api.bestinslot.xyz/v3/mempool/all\_runic\_utxos

{% tabs %}
{% tab title="200: OK Success" %}
```json
{
    "data": [
        {
            "txid": "a63fa5a8d71f255d7ce5b699cbd4f21ed18014f0aa64df3f2eaf16bb2ad8213e",
            "vout": 0,
            "block_height": null,
            "value": 294,
            "address": "bc1q8ys49pxp3c6um7enemwdkl4ud5fwwg2rpdegxu",
            "script": "001439215284c18e35cdfb33cedcdb7ebc6d12e72143",
            "script_type": "witness_v0_keyhash",
            "inscription_ids": null,
            "satpoints": null,
            "rune_ids": [
                "1:0"
            ],
            "amounts": [
                "1"
            ],
            "txfee": "272",
            "vsize": 194,
            "utxo": "a63fa5a8d71f255d7ce5b699cbd4f21ed18014f0aa64df3f2eaf16bb2ad8213e:0"
        },
        ...
    ],
    "block_height": 889388
}
```
{% endtab %}
{% endtabs %}



## Get All Runes Events in Mempool

_<mark style="color:blue;">Included in: Pro, Dedicated</mark>_

<mark style="color:blue;">`GET`</mark> `https://api.bestinslot.xyz/v3/mempool/all_runes_events`

Returns all Runes Events in Mempool.

Sample query: https://api.bestinslot.xyz/v3/mempool/all\_runes\_events

{% tabs %}
{% tab title="200: OK Success" %}
```json
{
    "data": [
        {
            "event_type": "input",
            "txid": "081173c52b85daf229d7dd593e547886d31dd9bc73cf712ecb8ef225f11b6561",
            "outpoint": "96b5d45828720428f3853419250f15a72eb6feebd29d26b5f9e361bdb42a0e94:0",
            "pkscript": "001439215284c18e35cdfb33cedcdb7ebc6d12e72143",
            "wallet_addr": "bc1q8ys49pxp3c6um7enemwdkl4ud5fwwg2rpdegxu",
            "rune_id": "1:0",
            "amount": "1",
            "rune_name": "UNCOMMONGOODS",
            "spaced_rune_name": "UNCOMMON•GOODS",
            "decimals": 0,
            "sale_info": null
        },
        ...
    ],
    "block_height": 889389
}
```
{% endtab %}
{% endtabs %}
