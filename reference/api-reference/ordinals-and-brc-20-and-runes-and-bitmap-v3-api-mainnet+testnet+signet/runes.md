---
description: Endpoints related to Runes Protocol.
---

# Runes

Endpoints' API-Key-Tier availabilities are written for each endpoint.

**To use on testnet4/signet, use your current api-key and send the request to `https://testnet.api.bestinslot.xyz` / `https://signet_api.bestinslot.xyz`**

## **Terminology**

\<Used in this API for standardization> : \<Terminology in Runes>

* rune\_name: Non-spaced unique Rune Name
* deploy\_txid: etching
* decimals: divisibility
* per\_mint\_amount: terms.amount (each mint event mints this amount for this rune)
* mint\_cnt: mints (count of mint events)
* mint\_cnt\_limit: terms.cap (maximum allowed mint events for this rune)
* premined\_supply: premine (rune amount mined while deploying the rune)
* total\_minted\_supply: premine + mint\_cnt \* per\_mint\_amount
* circulating\_supply: premine + mint\_cnt \* per\_mint\_amount - burned\_supply
* mintable: mint\_cnt < mint\_cnt\_limit & (mint\_start\_block <= current\_block < mint\_end\_block)
* auto\_upgrade: turbo (should ticker auto opt-in to new runes features)
* output => \<txid>:\<output\_index>
* pkscript => bitcoin ScriptPubKey
* avg\_unit\_price\_in\_sats => Calculated by taking the median unit price of sales in last 6 hrs. If there are not enough sale in last 6 hrs, it'll look at latest several sales, if there is not enough sale on the ticker, it'll return null. Note that this is scaled by decimals to make ordering more meaningful.
* event\_type => possible options are: input, new-allocation, mint, output, burn

## Runes Testnet4 Faucet (only on testnet)

_<mark style="color:blue;">Included in: Basic, Pro, Dedicated</mark>_

<mark style="color:blue;">`GET`</mark> `https://testnet.api.bestinslot.xyz/v3/runes/testnet_faucet`

A testnet rune faucet that mints 1.0 (1\_0000\_0000) test rune to target address.

**NOTE: Limited with 10 request per 24 hours per key.**

Sample query: https://testnet.api.bestinslot.xyz/v3/runes/testnet\_faucet?address=tb1qvhl8k0xu0stk956tjqx6q5ujp6tdyh24xcz0qq

#### Query Parameters

| Name                                      | Type     | Description                    |
| ----------------------------------------- | -------- | ------------------------------ |
| address<mark style="color:red;">\*</mark> | `string` | Testnet Bitcoin wallet address |

**Response**

{% tabs %}
{% tab title="200: OK Success" %}
```json
{
    "mint_txid": "43cec273ded990afcc681eb64da2e4884f7dc8518db01f82620dff98beaa0e49"
}
```
{% endtab %}
{% endtabs %}



## Runes Tickers

_<mark style="color:blue;">Included in: Basic, Pro, Dedicated</mark>_

<mark style="color:blue;">`GET`</mark> `https://api.bestinslot.xyz/v3/runes/tickers`

Returns information about runes tickers.

**NOTE:** `avg_unit_price_in_sats` is scaled by decimals to make ordering more meaningful.

Sample query: https://api.bestinslot.xyz/v3/runes/tickers?sort\_by=rune\_number\&order=asc\&offset=0\&count=100

#### Query Parameters

<table><thead><tr><th width="168">Name</th><th width="232">Type</th><th>Description</th></tr></thead><tbody><tr><td>sort_by<mark style="color:red;">*</mark></td><td><code>string</code></td><td>rune_id, rune_number, rune_name, mint_cnt, total_minted_supply, burned_supply, circulating_supply, mint_progress, deploy_ts, holder_count, event_count<br><br>PRO TIER:<br>avg_unit_price_in_sats, min_listed_unit_price_in_sats, min_listed_unit_price_unisat, listed_supply, listed_supply_ratio, marketcap, total_volume</td></tr><tr><td>order<mark style="color:red;">*</mark></td><td><code>string</code></td><td>asc, desc</td></tr><tr><td>offset<mark style="color:red;">*</mark></td><td><code>int</code></td><td>0 &#x3C;= offset</td></tr><tr><td>count<mark style="color:red;">*</mark></td><td><code>int</code></td><td>20 &#x3C;= count &#x3C;= 300</td></tr><tr><td>minting_status</td><td><code>string</code></td><td>(optional)<br>set to "not_complete" for searching only the tickers with mintable = true<br><br>set to "completed" for searching only the tickers with mintable = false<br><br>leave unset to search within all tickers</td></tr></tbody></table>

**Response**

{% tabs %}
{% tab title="200: OK Success" %}
```json
{
    "data": [
        {
            "rune_id": "840000:1",
            "rune_number": "1",
            "rune_name": "ZZZZZFEHUZZZZZ",
            "spaced_rune_name": "Z•Z•Z•Z•Z•FEHU•Z•Z•Z•Z•Z",
            "symbol": "ᚠ",
            "decimals": 2,
            "per_mint_amount": "100",
            "mint_cnt": "1111111",
            "mint_cnt_limit": "1111111",
            "premined_supply": "11000000000",
            "total_minted_supply": "11111111100",
            "burned_supply": "46300",
            "circulating_supply": "11111064800",
            "mint_progress": 100,
            "mint_start_block": null,
            "mint_end_block": null,
            "genesis_block": 840000,
            "deploy_ts": "2024-04-20T00:09:27.000Z",
            "deploy_txid": "2bb85f4b004be6da54f766c17c1e855187327112c231ef2ff35ebad0ea67c69e",
            "auto_upgrade": true,
            "holder_count": 22865,
            "event_count": 3033717,
            "mintable": false,
            "icon_inscr_id": "2bb85f4b004be6da54f766c17c1e855187327112c231ef2ff35ebad0ea67c69ei0",
            "icon_delegate_id": "e16b8b872584112c6e84c5a941e8ad91f9e428458605a0e9f582305dd12ef247i0",
            "icon_content_url": "https://bis-ord-content.fra1.cdn.digitaloceanspaces.com/ordinals/e16b8b872584112c6e84c5a941e8ad91f9e428458605a0e9f582305dd12ef247i0",
            "icon_render_url": null,
            "avg_unit_price_in_sats": 30195.999999999996,
            "min_listed_unit_price_in_sats": 30233.581818181818,
            "min_listed_unit_price_unisat": 30233.582000000002,
            "listed_supply": "929250",
            "listed_supply_ratio": 0.00008363284858171289,
            "marketcap": 3355097127008,
            "total_sale_info": {
                "sale_count": 106570,
                "sale_count_3h": 0,
                "sale_count_6h": 1,
                "sale_count_9h": 1,
                "sale_count_12h": 73,
                "sale_count_1d": 205,
                "sale_count_3d": 413,
                "sale_count_7d": 1002,
                "sale_count_30d": 2583,
                "sale_amount": 77883929,
                "vol_3h": 0,
                "vol_6h": 126159,
                "vol_9h": 126159,
                "vol_12h": 1226131,
                "vol_1d": 4207823,
                "vol_3d": 16909211,
                "vol_7d": 51653484,
                "vol_30d": 220929558,
                "vol_total": 26566160622
            }
        },
        ...
    ],
    "block_height": 847620
}
```
{% endtab %}

{% tab title="429: Too Many Requests Rate limit exceeded" %}
```json
```
{% endtab %}
{% endtabs %}



## Runes Ticker Count

_<mark style="color:blue;">Included in: Basic, Pro, Dedicated</mark>_

<mark style="color:blue;">`GET`</mark> `https://api.bestinslot.xyz/v3/runes/ticker_cnt`

Returns count of all runes tickers and mintable runes tickers

Sample query: https://api.bestinslot.xyz/v3/runes/ticker\_cnt

{% tabs %}
{% tab title="200: OK Success" %}
```json
{
    "data": {
        "ticker_cnt": 70480,
        "minting_ticker_cnt": 14596
    },
    "block_height": 844739
}
```
{% endtab %}
{% endtabs %}



## Runes Single Ticker Info

_<mark style="color:blue;">Included in: Basic, Pro, Dedicated</mark>_

<mark style="color:blue;">`GET`</mark> `https://api.bestinslot.xyz/v3/runes/ticker_info`

Returns information about given runes ticker.

<mark style="color:orange;">NOTE: avg\_unit\_price\_in\_sats, min\_listed\_unit\_price\_in\_sats, listed\_supply, listed\_supply\_ratio, marketcap and total\_sale\_info are only available in PRO tier.</mark>

Sample query: https://api.bestinslot.xyz/v3/runes/ticker\_info?rune\_name=UNCOMMONGOODS

#### Query Parameters

| Name         | Type     | Description                        |
| ------------ | -------- | ---------------------------------- |
| rune\_name   | `string` | (optional) Non-Spaced name of Rune |
| rune\_id     | `string` | (optional) Rune ID                 |
| rune\_number | `int`    | (optional) Rune Number             |

**NOTE: One of rune\_name, rune\_id or rune\_number must be specified**

**Response**

{% tabs %}
{% tab title="200: OK Success" %}
```json
{
    "data": {
        "rune_id": "840000:1",
        "rune_number": "1",
        "rune_name": "ZZZZZFEHUZZZZZ",
        "spaced_rune_name": "Z•Z•Z•Z•Z•FEHU•Z•Z•Z•Z•Z",
        "symbol": "ᚠ",
        "decimals": 2,
        "per_mint_amount": "100",
        "mint_cnt": "1111111",
        "mint_cnt_limit": "1111111",
        "premined_supply": "11000000000",
        "total_minted_supply": "11111111100",
        "burned_supply": "46300",
        "circulating_supply": "11111064800",
        "mint_progress": 100,
        "mint_start_block": null,
        "mint_end_block": null,
        "genesis_block": 840000,
        "deploy_ts": "2024-04-20T00:09:27.000Z",
        "deploy_txid": "2bb85f4b004be6da54f766c17c1e855187327112c231ef2ff35ebad0ea67c69e",
        "auto_upgrade": true,
        "holder_count": 22865,
        "event_count": 3033717,
        "mintable": false,
        "icon_inscr_id": "2bb85f4b004be6da54f766c17c1e855187327112c231ef2ff35ebad0ea67c69ei0",
        "icon_delegate_id": "e16b8b872584112c6e84c5a941e8ad91f9e428458605a0e9f582305dd12ef247i0",
        "icon_content_url": "https://bis-ord-content.fra1.cdn.digitaloceanspaces.com/ordinals/e16b8b872584112c6e84c5a941e8ad91f9e428458605a0e9f582305dd12ef247i0",
        "icon_render_url": null,
        "avg_unit_price_in_sats": 30195.999999999996,
        "min_listed_unit_price_in_sats": 30233.581818181818,
        "min_listed_unit_price_unisat": 30233.582000000002,
        "listed_supply": "929250",
        "listed_supply_ratio": 0.00008363284858171289,
        "marketcap": 3355097127008,
        "total_sale_info": {
            "sale_count": 106570,
            "sale_count_3h": 0,
            "sale_count_6h": 1,
            "sale_count_9h": 1,
            "sale_count_12h": 73,
            "sale_count_1d": 205,
            "sale_count_3d": 413,
            "sale_count_7d": 1002,
            "sale_count_30d": 2583,
            "sale_amount": 77883929,
            "vol_3h": 0,
            "vol_6h": 126159,
            "vol_9h": 126159,
            "vol_12h": 1226131,
            "vol_1d": 4207823,
            "vol_3d": 16909211,
            "vol_7d": 51653484,
            "vol_30d": 220929558,
            "vol_total": 26566160622
        }
    },
    "block_height": 847620
}
```
{% endtab %}

{% tab title="429: Too Many Requests Rate limit exceeded" %}
```json
```
{% endtab %}
{% endtabs %}



## Get Runes Sales Information

_<mark style="color:blue;">Included in: Pro, Dedicated</mark>_

<mark style="color:blue;">`GET`</mark> `https://api.bestinslot.xyz/v3/runes/sales_info`

Returns sales and volume information about a specific runes ticker.

Sample query: https://api.bestinslot.xyz/v3/runes/sales\_info?rune\_name=SATOSHINAKAMOTO\&marketplace\_type=unisat

#### Query Parameters

| Name              | Type     | Description                                                                                      |
| ----------------- | -------- | ------------------------------------------------------------------------------------------------ |
| rune\_name        | `string` | (optional) Non-Spaced name of Rune                                                               |
| rune\_id          | `string` | (optional) Rune ID                                                                               |
| rune\_number      | `int`    | (optional) Rune Number                                                                           |
| marketplace\_type | `string` | (optional) Filter only by a given marketplace. You can find the allowed types on Constants Page. |

**NOTE: One of rune\_name, rune\_id or rune\_number must be specified**

{% tabs %}
{% tab title="200: OK Success" %}
```json
{
    "data": {
        "marketplace": "all",
        "vol_3h": 7579717,
        "vol_6h": 15354385,
        "vol_9h": 24536418,
        "vol_12h": 43035106,
        "vol_1d": 63367091,
        "vol_3d": 149531954,
        "vol_7d": 397417106,
        "vol_30d": 2320019379,
        "vol_total": 12611770343,
        "sale_count": 55463, // how many sales have happened
        "sale_count_3h": 32,
        "sale_count_6h": 78,
        "sale_count_9h": 158,
        "sale_count_12h": 265,
        "sale_count_1d": 361,
        "sale_count_3d": 925,
        "sale_count_7d": 1915,
        "sale_count_30d": 8374,
        "sale_amount": 19261486 // the total amount of tokens sold
    },
    "block_height": 862524
}
```
{% endtab %}
{% endtabs %}



## Get Runes Market Information

_<mark style="color:blue;">Included in: Pro, Dedicated</mark>_

<mark style="color:blue;">`GET`</mark> `https://api.bestinslot.xyz/v3/runes/market_info`

Returns market information about a specific runes ticker.

Sample query: https://api.bestinslot.xyz/v3/runes/market\_info?rune\_name=SATOSHINAKAMOTO

#### Query Parameters

| Name         | Type     | Description                        |
| ------------ | -------- | ---------------------------------- |
| rune\_name   | `string` | (optional) Non-Spaced name of Rune |
| rune\_id     | `string` | (optional) Rune ID                 |
| rune\_number | `int`    | (optional) Rune Number             |

**NOTE: One of rune\_name, rune\_id or rune\_number must be specified**

{% tabs %}
{% tab title="200: OK Success" %}
```json
{
    "data": {
        "marketcap": 71876303181,
        "min_listed_unit_price_in_sats": 3308.5,
        "min_listed_unit_price_unisat": 3308.5,
        "listed_supply": "35785835289050",
        "listed_supply_ratio": 0.017041117391700833
    },
    "block_height": 841495
}
```
{% endtab %}
{% endtabs %}



## Runes Listings

_<mark style="color:blue;">Included in: Pro, Dedicated</mark>_

<mark style="color:blue;">`GET`</mark> `https://api.bestinslot.xyz/v3/runes/listings`

Returns listing information of a given rune.

Sample query: https://api.bestinslot.xyz/v3/runes/listings?rune\_id=840000:3\&sort\_by=min\_unit\_price\&order=asc\&offset=0\&count=100

#### Query Parameters

<table><thead><tr><th width="244">Name</th><th>Type</th><th>Description</th></tr></thead><tbody><tr><td>rune_name</td><td><code>string</code></td><td>(optional) Non-Spaced name of Rune</td></tr><tr><td>rune_id</td><td><code>string</code></td><td>(optional) Rune ID</td></tr><tr><td>rune_number</td><td><code>int</code></td><td>(optional) Rune Number</td></tr><tr><td>sort_by<mark style="color:red;">*</mark></td><td><code>string</code></td><td>output, min_price, unisat_price</td></tr><tr><td>order<mark style="color:red;">*</mark></td><td><code>string</code></td><td>asc, desc</td></tr><tr><td>offset<mark style="color:red;">*</mark></td><td><code>int</code></td><td>0 &#x3C;= offset</td></tr><tr><td>count<mark style="color:red;">*</mark></td><td><code>int</code></td><td>20 &#x3C;= count &#x3C;= 100</td></tr></tbody></table>

**NOTE: One of rune\_name, rune\_id or rune\_number must be specified.**

**Response**

{% tabs %}
{% tab title="200: OK Success" %}
```json
{
    "data": [
        {
            "outpoint": "e03a893219770a198903430634e998c2e7ccaf4fb7a4e8713421f2020822f54c:2",
            "owner_wallet_addr": "bc1pp7sp50mpsew65ax6x6vjymv7ltsv88xjlzuxnlruca3vkggnggxs43tak5",
            "amount": 5000000,
            "min_price": 26875200,
            "min_unit_price": 5.37504,
            "unisat_price": 26875200,
            "unisat_unit_price": 5.37504
        },
        ...
    ],
    "block_height": 840350
}
```
{% endtab %}
{% endtabs %}



## Runes Holders

_<mark style="color:blue;">Included in: Basic, Pro, Dedicated</mark>_

<mark style="color:blue;">`GET`</mark> `https://api.bestinslot.xyz/v3/runes/holders`

Returns balances of holders of a given runes ticker.

Sample query: https://api.bestinslot.xyz/v3/runes/holders?rune\_name=UNCOMMONGOODS\&sort\_by=balance\&order=desc\&count=500\&offset=0

#### Query Parameters

| Name                                       | Type     | Description                            |
| ------------------------------------------ | -------- | -------------------------------------- |
| rune\_name                                 | `string` | (optional) Non-Spaced name of Rune     |
| rune\_id                                   | `string` | (optional) Rune ID                     |
| rune\_number                               | int      | (optional) Rune Number                 |
| sort\_by<mark style="color:red;">\*</mark> | `string` | currently only option is `balance`     |
| order<mark style="color:red;">\*</mark>    | `string` | asc, desc                              |
| offset<mark style="color:red;">\*</mark>   | `int`    | 0 <= offset                            |
| count<mark style="color:red;">\*</mark>    | `int`    | 20 <= count <= 500 (5000 for PRO Keys) |

**NOTE: One of rune\_name, rune\_id or rune\_number must be specified**

**Response**

{% tabs %}
{% tab title="200: OK Success" %}
```json
{
    "data": [
        {
            "pkscript": "5120851d39de85d2454d267c707d18970fc9dc680fc237e42d1d271a01db230a0195",
            "wallet_addr": "bc1ps5wnnh596fz56fnuwp7339c0e8wxsr7zxljz68f8rgqakgc2qx2stuz5yu",
            "rune_id": "1:0",
            "total_balance": "10000",
            "rune_name": "UNCOMMONGOODS",
            "spaced_rune_name": "UNCOMMON•GOODS",
            "decimals": 0
        },
        ...
    ],
    "block_height": 840523
}
```
{% endtab %}

{% tab title="429: Too Many Requests Rate limit exceeded" %}

{% endtab %}
{% endtabs %}



## Runes Single Output Info

_<mark style="color:blue;">Included in: Basic, Pro, Dedicated</mark>_

<mark style="color:blue;">`GET`</mark> `https://api.bestinslot.xyz/v3/runes/output_info`

Returns runes information about given bitcoin output.

Sample query: https://api.bestinslot.xyz/v3/runes/output\_info?output=314e5e53024ec5860bd2fa2a4e85db2fc9097fcf58caa63f253bb4f86ad4b412:1

#### Query Parameters

| Name                                     | Type     | Description                         |
| ---------------------------------------- | -------- | ----------------------------------- |
| output<mark style="color:red;">\*</mark> | `string` | Outpoint to check runes information |

**Response**

{% tabs %}
{% tab title="200: OK Success" %}
```json
{
    "data": {
        "pkscript": "512024034ada955f1716ed7833d56744bd08119355cf5b1bbdbc48e66bc357bdb3b7",
        "wallet_addr": "bc1pysp54k54tut3dmtcx02kw39apqgex4w0tvdmm0zgue4ux4aakwms3pumq8",
        "output": "4ee2151d7010574cadc749ce85ae813599c33fc62148a0352eaa946f2da1d2be:0",
        "rune_ids": [
            "840000:22"
        ],
        "balances": [
            "190000000000"
        ],
        "spent": false,
        "rune_names": [
            "SATOSHINAKAMOTO"
        ],
        "spaced_rune_names": [
            "SATOSHI•NAKAMOTO"
        ],
        "decimals": [
            8
        ]
    },
    "block_height": 840523
}
```
{% endtab %}

{% tab title="429: Too Many Requests Rate limit exceeded" %}

{% endtab %}
{% endtabs %}



## Runes Batch Output Info

_<mark style="color:blue;">Included in: Basic, Pro, Dedicated</mark>_

<mark style="color:green;">`POST`</mark> `https://api.bestinslot.xyz/v3/runes/batch_output_info`

Returns runes information about given bitcoin outputs.

Sample query: \
url: \
`https://api.bestinslot.xyz/v3/runes/batch_output_info`

data: \
`{ "queries": [ "314e5e53024ec5860bd2fa2a4e85db2fc9097fcf58caa63f253bb4f86ad4b412:1", "0979edfb33fa380fb8c80e53809e9d865169ac6857688b31446d577d5f6df869:1", "200380702f43b2a6403bd9576c48e74e7cf184d5ead280eaa25a2d71be9cb2c8:1" ] }`

headers: \
`{ "Content-Type":"application/json", "x-api-key":"...." }`

#### Request Body

| Name                                      | Type    | Description                                         |
| ----------------------------------------- | ------- | --------------------------------------------------- |
| queries<mark style="color:red;">\*</mark> | `array` | <p>Array of outpoint strings<br>Max length: 100</p> |

**Response**

{% tabs %}
{% tab title="200: OK Success" %}
```json
{
    "data": [
        {
            "pkscript": "512024034ada955f1716ed7833d56744bd08119355cf5b1bbdbc48e66bc357bdb3b7",
            "wallet_addr": "bc1pysp54k54tut3dmtcx02kw39apqgex4w0tvdmm0zgue4ux4aakwms3pumq8",
            "output": "4ee2151d7010574cadc749ce85ae813599c33fc62148a0352eaa946f2da1d2be:0",
            "rune_ids": [
                "840000:22"
            ],
            "balances": [
                "190000000000"
            ],
            "spent": false,
            "rune_names": [
                "SATOSHINAKAMOTO"
            ],
            "spaced_rune_names": [
                "SATOSHI•NAKAMOTO"
            ],
            "decimals": [
                8
            ]
        },
        ...
    ],
    "block_height": 840350
}
```
{% endtab %}
{% endtabs %}



## Runes Wallet Balances

_<mark style="color:blue;">Included in: Basic, Pro, Dedicated</mark>_

<mark style="color:blue;">`GET`</mark> `https://api.bestinslot.xyz/v3/runes/wallet_balances`

Returns runes balance information about given bitcoin wallet address or pkscript.

**NOTE:** `avg_unit_price_in_sats` and `min_listed_unit_price_in_sats` is scaled by decimals.

Sample query: https://api.bestinslot.xyz/v3/runes/wallet\_balances?address=tb1pd368q84tuark4naym2u5382p59jkd27nw5vu5s44uz8dwdlrcwhqzdl2l2

#### Query Parameters

| Name     | Type     | Description                         |
| -------- | -------- | ----------------------------------- |
| address  | `string` | (optional) Bitcoin wallet address   |
| pkscript | `string` | (optional) Bitcoin script\_pub\_key |

**NOTE: One of address or pkscript must be specified**

**Response**

{% tabs %}
{% tab title="200: OK Success" %}
```json
{
    "data": [
        {
            "pkscript": "512024034ada955f1716ed7833d56744bd08119355cf5b1bbdbc48e66bc357bdb3b7",
            "wallet_addr": "bc1pysp54k54tut3dmtcx02kw39apqgex4w0tvdmm0zgue4ux4aakwms3pumq8",
            "rune_id": "840000:22",
            "total_balance": "4120000000000",
            "rune_name": "SATOSHINAKAMOTO",
            "spaced_rune_name": "SATOSHI•NAKAMOTO",
            "decimals": 8,
            "avg_unit_price_in_sats": 3422.7299999999996,
            "min_listed_unit_price_in_sats": 3308.5,
            "min_listed_unit_price_unisat": 3308.5
        },
        ...
    ],
    "block_height": 840350
}
```
{% endtab %}
{% endtabs %}



## Runes Wallet Valid Outputs

_<mark style="color:blue;">Included in: Basic, Pro, Dedicated</mark>_

<mark style="color:blue;">`GET`</mark> `https://api.bestinslot.xyz/v3/runes/wallet_valid_outputs`

Returns unspent output information of a given wallet.

Sample query: https://api.bestinslot.xyz/v3/runes/wallet\_valid\_outputs?pkscript=51206c74701eabe7476acfa4dab9489d41a16566abd37519ca42b5e08ed737e3c3ae\&sort\_by=output\&order=asc\&offset=0\&count=2000

#### Query Parameters

<table><thead><tr><th width="244">Name</th><th>Type</th><th>Description</th></tr></thead><tbody><tr><td>address</td><td><code>string</code></td><td>(optional) Bitcoin wallet address</td></tr><tr><td>pkscript</td><td><code>string</code></td><td>(optional) Bitcoin script_pub_key</td></tr><tr><td>sort_by<mark style="color:red;">*</mark></td><td><code>string</code></td><td>output, min_price, unisat_price</td></tr><tr><td>order<mark style="color:red;">*</mark></td><td><code>string</code></td><td>asc, desc</td></tr><tr><td>offset<mark style="color:red;">*</mark></td><td><code>int</code></td><td>0 &#x3C;= offset</td></tr><tr><td>count<mark style="color:red;">*</mark></td><td><code>int</code></td><td>20 &#x3C;= count &#x3C;= 2000</td></tr></tbody></table>

**NOTE: One of address or pkscript must be specified**

**Response**

{% tabs %}
{% tab title="200: OK Success" %}
```json
{
    "data": [
        {
            "pkscript": "5120ef4a9ffbb9a627f495a3f224f0d728476890198813d97935febbc539a4a6608e",
            "wallet_addr": "bc1paa9fl7ae5cnlf9dr7gj0p4egga5fqxvgz0vhjd07h0znnf9xvz8qfsw3e8",
            "output": "2d69dca0ce6ff19dcd1bddaf56e3760c106a62832d81611c5aa0501966af7aa2:1",
            "rune_ids": [
                "840000:3"
            ],
            "balances": [
                "173424909679"
            ],
            "min_price": 9533514,
            "unisat_price": 9533514,
            "rune_names": [
                "DOGGOTOTHEMOON"
            ],
            "spaced_rune_names": [
                "DOG•GO•TO•THE•MOON"
            ],
            "decimals": [
                5
            ]
        },
        ...
    ],
    "block_height": 840350
}
```
{% endtab %}
{% endtabs %}



## Runes Wallet Valid Outputs Single Rune

_<mark style="color:blue;">Included in: Basic, Pro, Dedicated</mark>_

<mark style="color:blue;">`GET`</mark> `https://api.bestinslot.xyz/v3/runes/wallet_valid_outputs_single_rune`

Returns unspent output information of a given wallet of a given rune.

Sample query: https://api.bestinslot.xyz/v3/runes/wallet\_valid\_outputs\_single\_rune?address=bc1paa9fl7ae5cnlf9dr7gj0p4egga5fqxvgz0vhjd07h0znnf9xvz8qfsw3e8\&sort\_by=min\_price\&order=asc\&offset=0\&count=2000\&rune\_id=840000:3

#### Query Parameters

<table><thead><tr><th width="244">Name</th><th>Type</th><th>Description</th></tr></thead><tbody><tr><td>rune_name</td><td><code>string</code></td><td>(optional) Non-Spaced name of Rune</td></tr><tr><td>rune_id</td><td><code>string</code></td><td>(optional) Rune ID</td></tr><tr><td>rune_number</td><td><code>int</code></td><td>(optional) Rune Number</td></tr><tr><td>address</td><td><code>string</code></td><td>(optional) Bitcoin wallet address</td></tr><tr><td>pkscript</td><td><code>string</code></td><td>(optional) Bitcoin script_pub_key</td></tr><tr><td>sort_by<mark style="color:red;">*</mark></td><td><code>string</code></td><td>output, min_price, unisat_price</td></tr><tr><td>order<mark style="color:red;">*</mark></td><td><code>string</code></td><td>asc, desc</td></tr><tr><td>offset<mark style="color:red;">*</mark></td><td><code>int</code></td><td>0 &#x3C;= offset</td></tr><tr><td>count<mark style="color:red;">*</mark></td><td><code>int</code></td><td>20 &#x3C;= count &#x3C;= 2000</td></tr></tbody></table>

**NOTE: One of address or pkscript must be specified, one of rune\_name, rune\_id or rune\_number must be specified**

**Response**

{% tabs %}
{% tab title="200: OK Success" %}
```json
{
    "data": [
        {
            "pkscript": "5120ef4a9ffbb9a627f495a3f224f0d728476890198813d97935febbc539a4a6608e",
            "wallet_addr": "bc1paa9fl7ae5cnlf9dr7gj0p4egga5fqxvgz0vhjd07h0znnf9xvz8qfsw3e8",
            "output": "2d69dca0ce6ff19dcd1bddaf56e3760c106a62832d81611c5aa0501966af7aa2:1",
            "rune_ids": [
                "840000:3"
            ],
            "balances": [
                "173424909679"
            ],
            "balance_of_rune": "173424909679",
            "min_price": 9533514,
            "min_unit_price": 5.497199922229171,
            "unisat_price": 9533514,
            "unisat_unit_price": 5.497199927995356,
            "rune_names": [
                "DOGGOTOTHEMOON"
            ],
            "spaced_rune_names": [
                "DOG•GO•TO•THE•MOON"
            ],
            "decimals": [
                5
            ]
        },
        ...
    ],
    "block_height": 840350
}
```
{% endtab %}
{% endtabs %}



## Runes Valid Outputs

_<mark style="color:blue;">Included in: Basic, Pro, Dedicated</mark>_

<mark style="color:blue;">`GET`</mark> `https://api.bestinslot.xyz/v3/runes/valid_outputs`

Returns unspent output information of a given ticker.

Sample query: https://api.bestinslot.xyz/v3/runes/valid\_outputs?rune\_name=UNCOMMONGOODS\&sort\_by=output\&order=asc\&offset=0\&count=2000

#### Query Parameters

| Name                                       | Type     | Description                                                                      |
| ------------------------------------------ | -------- | -------------------------------------------------------------------------------- |
| rune\_name                                 | `string` | (optional) Non-Spaced name of Rune                                               |
| rune\_id                                   | `string` | (optional) Rune ID                                                               |
| rune\_number                               | `int`    | (optional) Rune Number                                                           |
| sort\_by<mark style="color:red;">\*</mark> | `string` | output, amount, min\_price, min\_unit\_price, unisat\_price, unisat\_unit\_price |
| order<mark style="color:red;">\*</mark>    | `string` | asc, desc                                                                        |
| offset<mark style="color:red;">\*</mark>   | `int`    | 0 <= offset                                                                      |
| count<mark style="color:red;">\*</mark>    | `int`    | 20 <= count <= 2000                                                              |

**NOTE: One of rune\_name, rune\_id or rune\_number must be specified**

**Response**

{% tabs %}
{% tab title="200: OK Success" %}
```json
{
    "data": [
        {
            "output": "ccb6b5af0499b6626928e2c7aa4c725307fea8ae6dd89fea1ee34bc6e58ecb78:2",
            "pkscript": "512059097d303921cee03ed48b99637ce90c446576b5c89ac85371a44a08a96c7860",
            "wallet_addr": "bc1ptyyh6vpey88wq0k53wvkxl8fp3zx2a44ezdvs5m3539q32tv0psq4k86ef",
            "rune_ids": [
                "840000:22"
            ],
            "balances": [
                "60000000000"
            ],
            "balance_of_rune": "60000000000",
            "min_price": 1985100,
            "min_unit_price": 3308.5,
            "unisat_price": 1985100,
            "unisat_unit_price": 3308.5,
            "rune_names": [
                "SATOSHINAKAMOTO"
            ],
            "spaced_rune_names": [
                "SATOSHI•NAKAMOTO"
            ],
            "decimals": [
                8
            ]
        },
        ...
    ],
    "block_height": 840523
}
```
{% endtab %}
{% endtabs %}



## Runes Wallet Activity

_<mark style="color:blue;">Included in: Pro, Dedicated</mark>_

<mark style="color:blue;">`GET`</mark> `https://api.bestinslot.xyz/v3/runes/wallet_activity`

Returns runes activity of a given wallet. If the given wallet is involved in a runes transaction, all activity in the transaction will be returned (even if that activity is an input/output to a different wallet)

The endpoint includes an optional rune filter. You can leave the parameters `rune_name`, `rune_id`, and `rune_number` blank to retrieve all wallet activity. Alternatively, you may supply at most one of these parameters to filter transactions where one of the events in the tx involves both the specified wallet and rune.

If optional `runes_filter_only_wallet` parameter is set to true, the endpoint only returns the runes events with the selected wallet. Otherwise it also includes the other runes events in the transaction.

Sample query: https://api.bestinslot.xyz/v3/runes/wallet\_activity?pkscript=51206c74701eabe7476acfa4dab9489d41a16566abd37519ca42b5e08ed737e3c3ae\&sort\_by=ts\&order=desc\&offset=0\&count=2000

#### Query Parameters

<table><thead><tr><th width="244">Name</th><th>Type</th><th>Description</th></tr></thead><tbody><tr><td>address</td><td><code>string</code></td><td>(optional) Bitcoin wallet address</td></tr><tr><td>pkscript</td><td><code>string</code></td><td>(optional) Bitcoin script_pub_key</td></tr><tr><td>rune_name</td><td><code>string</code></td><td>(optional) Non-Spaced name of Rune</td></tr><tr><td>rune_id</td><td><code>string</code></td><td>(optional) Rune ID</td></tr><tr><td>rune_number</td><td><code>int</code></td><td>(optional) Rune Number</td></tr><tr><td>sort_by<mark style="color:red;">*</mark></td><td><code>string</code></td><td>currently only option is <code>ts</code> (timestamp)</td></tr><tr><td>order<mark style="color:red;">*</mark></td><td><code>string</code></td><td>asc, desc</td></tr><tr><td>offset<mark style="color:red;">*</mark></td><td><code>int</code></td><td>0 &#x3C;= offset</td></tr><tr><td>count<mark style="color:red;">*</mark></td><td><code>int</code></td><td>20 &#x3C;= count &#x3C;= 2000</td></tr><tr><td>runes_filter_only_wallet</td><td><code>string</code></td><td>(optional) "true" or "false"</td></tr></tbody></table>

**NOTE: One of address or pkscript must be specified**

**Response**

{% tabs %}
{% tab title="200: OK Success" %}
```json
{
    "data": [
        {
            "event_type": "output",
            "txid": "6f77a8234c74559c2fa74b604bb8318a6811c288591b07e95adc381eb363320e",
            "outpoint": "6f77a8234c74559c2fa74b604bb8318a6811c288591b07e95adc381eb363320e:0",
            "pkscript": "512088de610b5857285c27fb45369ec8d4c56cf59b4b67ddebc9a7898987e7f82dcd",
            "wallet_addr": "bc1p3r0xzz6c2u59cflmg5mfajx5c4k0tx6tvlw7hjd83xyc0elc9hxslysx6c",
            "rune_id": "840000:22",
            "amount": "560000000000",
            "block_height": 840407,
            "block_timestamp": "2024-04-22T22:15:00.000Z",
            "rune_name": "SATOSHINAKAMOTO",
            "spaced_rune_name": "SATOSHI•NAKAMOTO",
            "decimals": 8,
            "sale_info": null,
            "icon_content_url": "https://bis-ord-content.fra1.cdn.digitaloceanspaces.com/ordinals/f753cefb770bf69369d33e93fbc9271f8dc877cb4819cbdd9d766f3509062e43i0",
            "icon_render_url": null
        },
        {
            "event_type": "input",
            "txid": "6f77a8234c74559c2fa74b604bb8318a6811c288591b07e95adc381eb363320e",
            "outpoint": "a914c7f595f6baac8e1d81b6cc3f0242607fa7686fabe04888f8c4f76927ab60:0",
            "pkscript": "512024034ada955f1716ed7833d56744bd08119355cf5b1bbdbc48e66bc357bdb3b7",
            "wallet_addr": "bc1pysp54k54tut3dmtcx02kw39apqgex4w0tvdmm0zgue4ux4aakwms3pumq8",
            "rune_id": "840000:22",
            "amount": "560000000000",
            "block_height": 840407,
            "block_timestamp": "2024-04-22T22:15:00.000Z",
            "rune_name": "SATOSHINAKAMOTO",
            "spaced_rune_name": "SATOSHI•NAKAMOTO",
            "decimals": 8,
            "sale_info": {
                "sale_price": 42560000,
                "sold_to_pkscript": "512088de610b5857285c27fb45369ec8d4c56cf59b4b67ddebc9a7898987e7f82dcd",
                "sold_to_wallet_addr": "bc1p3r0xzz6c2u59cflmg5mfajx5c4k0tx6tvlw7hjd83xyc0elc9hxslysx6c",
                "marketplace": "okx"
            },
            "icon_content_url": "https://bis-ord-content.fra1.cdn.digitaloceanspaces.com/ordinals/f753cefb770bf69369d33e93fbc9271f8dc877cb4819cbdd9d766f3509062e43i0",
            "icon_render_url": null
        },
        ...
    ],
    "block_height": 840350
}
```
{% endtab %}
{% endtabs %}



## Runes Activity of a Ticker

_<mark style="color:blue;">Included in: Pro, Dedicated</mark>_

<mark style="color:blue;">`GET`</mark> `https://api.bestinslot.xyz/v3/runes/activity`

Returns activity of a given ticker.

Sample query: https://api.bestinslot.xyz/v3/runes/activity?rune\_name=UNCOMMONGOODS\&sort\_by=ts\&order=desc\&offset=0\&count=2000

#### Query Parameters

| Name                                       | Type     | Description                        |
| ------------------------------------------ | -------- | ---------------------------------- |
| rune\_name                                 | `string` | (optional) Non-Spaced name of Rune |
| rune\_id                                   | `string` | (optional) Rune ID                 |
| rune\_number                               | `int`    | (optional) Rune Number             |
| sort\_by<mark style="color:red;">\*</mark> | `string` | output, amount                     |
| order<mark style="color:red;">\*</mark>    | `string` | asc, desc                          |
| offset<mark style="color:red;">\*</mark>   | `int`    | 0 <= offset                        |
| count<mark style="color:red;">\*</mark>    | `int`    | 20 <= count <= 2000                |

**NOTE: One of rune\_name, rune\_id or rune\_number must be specified**

**Response**

{% tabs %}
{% tab title="200: OK Success" %}
```json
{
    "data": [
        {
            "event_type": "output",
            "txid": "fa510ec0930c3eb4db1a92a84b237a10277db21e6fa4f3969c7bf8af5e73e4b6",
            "outpoint": "fa510ec0930c3eb4db1a92a84b237a10277db21e6fa4f3969c7bf8af5e73e4b6:1",
            "pkscript": "51209f8b1cf14c997a807d2c1509b39ff6f5f9d5b24cfd6dca5bba113ae995c840a1",
            "wallet_addr": "bc1pn793eu2vn9agqlfvz5ym88lk7huatvjvl4ku5ka6zyawn9wggzssv5n2ky",
            "rune_id": "840000:22",
            "amount": "200000000000",
            "block_height": 840350,
            "block_timestamp": "2024-04-22T13:46:20.000Z",
            "rune_name": "SATOSHINAKAMOTO",
            "spaced_rune_name": "SATOSHI•NAKAMOTO",
            "decimals": 8,
            "sale_info": null
        },
        {
            "event_type": "input",
            "txid": "fa510ec0930c3eb4db1a92a84b237a10277db21e6fa4f3969c7bf8af5e73e4b6",
            "outpoint": "1512857dabb0f6b7b2cdf9dfa867aa3e96eaa38bdc23527878c8de1e9c6fe7e3:2",
            "pkscript": "5120242129034b44bcc2c806cbb04ea34c43fb26b74c7429991e233ccb6bf046c821",
            "wallet_addr": "bc1pyssjjq6tgj7v9jqxewcyag6vg0ajdd6vws5ej83r8n9khuzxeqssp55n7m",
            "rune_id": "840000:22",
            "amount": "200000000000",
            "block_height": 840350,
            "block_timestamp": "2024-04-22T13:46:20.000Z",
            "rune_name": "SATOSHINAKAMOTO",
            "spaced_rune_name": "SATOSHI•NAKAMOTO",
            "decimals": 8,
            "sale_info": {
                "sale_price": 15754000,
                "sold_to_pkscript": "51209f8b1cf14c997a807d2c1509b39ff6f5f9d5b24cfd6dca5bba113ae995c840a1",
                "sold_to_wallet_addr": "bc1pn793eu2vn9agqlfvz5ym88lk7huatvjvl4ku5ka6zyawn9wggzssv5n2ky",
                "marketplace": "unisat"
            }
        },
        ...
    ],
    "block_height": 840350
}
```
{% endtab %}
{% endtabs %}



## Runes Activity in a Single Tx

_<mark style="color:blue;">Included in: Basic, Pro, Dedicated</mark>_

<mark style="color:blue;">`GET`</mark> `https://api.bestinslot.xyz/v3/runes/events_on_tx`

Returns runes activity on a given bitcoin transaction.

Sample query: https://api.bestinslot.xyz/v3/runes/events\_on\_tx?txid=e49f0912f94b915c0dd12b7970083b348945c2fc7bc01a21e0bfa403827607cf

#### Query Parameters

<table><thead><tr><th width="244">Name</th><th>Type</th><th>Description</th></tr></thead><tbody><tr><td>txid<mark style="color:red;">*</mark></td><td><code>string</code></td><td>Bitcoin txid</td></tr></tbody></table>

**Response**

{% tabs %}
{% tab title="200: OK Success" %}
```json
{
    "data": [
        {
            "event_type": "input",
            "txid": "34ff792cf5a50666fabfb8c2acc9ef8da9e5d180ab813713ad051d4117124333",
            "outpoint": "fa76b47040e0ed571030bff83713205167b6d1d2acba3bbb5f8fbaea09a4d4f9:0",
            "pkscript": "0014752451874597e90865c6e9b886b8640a36e82201",
            "wallet_addr": "bc1qw5j9rp69jl5ssewxaxugdwrypgmwsgspqhhttg",
            "rune_id": "840000:22",
            "amount": "20000000000",
            "block_height": 840336,
            "block_timestamp": "2024-04-22T11:47:44.000Z",
            "rune_name": "SATOSHINAKAMOTO",
            "spaced_rune_name": "SATOSHI•NAKAMOTO",
            "decimals": 8,
            "sale_info": {
                "sale_price": 1573800,
                "sold_to_pkscript": "5120e571909d0434b191f33cfcd7eb99f06e42a808594839fa7221594e86e212433b",
                "sold_to_wallet_addr": "bc1pu4cep8gyxjcerueulnt7hx0sdep2szzefqul5u3pt98gdcsjgvas8gtgrk",
                "marketplace": "unisat"
            }
        },
        {
            "event_type": "output",
            "txid": "34ff792cf5a50666fabfb8c2acc9ef8da9e5d180ab813713ad051d4117124333",
            "outpoint": "34ff792cf5a50666fabfb8c2acc9ef8da9e5d180ab813713ad051d4117124333:1",
            "pkscript": "5120e571909d0434b191f33cfcd7eb99f06e42a808594839fa7221594e86e212433b",
            "wallet_addr": "bc1pu4cep8gyxjcerueulnt7hx0sdep2szzefqul5u3pt98gdcsjgvas8gtgrk",
            "rune_id": "840000:22",
            "amount": "20000000000",
            "block_height": 840336,
            "block_timestamp": "2024-04-22T11:47:44.000Z",
            "rune_name": "SATOSHINAKAMOTO",
            "spaced_rune_name": "SATOSHI•NAKAMOTO",
            "decimals": 8,
            "sale_info": null
        }
    ],
    "block_height": 840350
}
```
{% endtab %}
{% endtabs %}



## Runes Historical Total Supply

_<mark style="color:blue;">Included in: Basic, Pro, Dedicated</mark>_

<mark style="color:blue;">`GET`</mark> `https://api.bestinslot.xyz/v3/runes/historical_total_supply`

Returns historical total supply for selected rune in selected block height.

Sample query: https://api.bestinslot.xyz/v3/runes/historical\_total\_supply?rune\_name=UNCOMMONGOODS\&block\_height=860000

#### Query Parameters

| Name                                            | Type     | Description                        |
| ----------------------------------------------- | -------- | ---------------------------------- |
| rune\_name                                      | `string` | (optional) Non-Spaced name of Rune |
| rune\_id                                        | `string` | (optional) Rune ID                 |
| rune\_number                                    | `int`    | (optional) Rune Number             |
| block\_height<mark style="color:red;">\*</mark> | `int`    | Bitcoin block height               |

**NOTE: One of rune\_name, rune\_id or rune\_number must be specified**

**Response**

{% tabs %}
{% tab title="200: OK Success" %}
```json
{
    "data": {
        "total_supply": "26035948",
        "block_height": "860000",
        "rune_id": "1:0",
        "decimals": 0
    },
    "block_height": 889396
}
```
{% endtab %}
{% endtabs %}



## Runes All Activity on Block Height

_<mark style="color:blue;">Included in: Enterprise, Dedicated</mark>_

<mark style="color:blue;">`GET`</mark> `https://api.bestinslot.xyz/v3/runes/activity_on_block`

Returns all runes activity in a given block height.

Sample query: https://api.bestinslot.xyz/v3/runes/activity\_on\_block?block\_height=840000

#### Query Parameters

| Name                                            | Type     | Description          |
| ----------------------------------------------- | -------- | -------------------- |
| block\_height<mark style="color:red;">\*</mark> | `string` | Bitcoin block height |

**Response**

{% tabs %}
{% tab title="200: OK Success" %}
```json
{
    "data": [
        {
            "event_type": "input",
            "txid": "e712da809a70f59067c3a65c16f7337079a1113e0072acbef50d96b4af9751a0",
            "outpoint": "6aea2e2992a65c1974c76a06a87412939b7629c884d07f1d8b09a531e45a32f9:1",
            "pkscript": "51201ac61709cc243d38f261a864fe9182e84b1b16df768a16077766e85942a9d1aa",
            "wallet_addr": "bc1prtrpwzwvys7n3unp4pj0ayvzap93k9klw69pvpmhvm59js4f6x4qy70yt8",
            "rune_id": "840000:453",
            "amount": "6666",
            "block_height": 840163,
            "block_timestamp": "2024-04-21T05:48:31.000Z",
            "rune_name": "ORDINALSAREDEAD",
            "spaced_rune_name": "ORDINALS•ARE•DEAD",
            "decimals": 0,
            "sale_info": {
                "sale_price": 79992,
                "sold_to_pkscript": "0014878ff1580d7ceedcd97e1b3cfa7cc0feef2b8f4d",
                "sold_to_wallet_addr": "bc1qs78lzkqd0nhdekt7rv705lxqlmhjhr6dggcdr4",
                "marketplace": "okx"
            }
        },
        {
            "event_type": "output",
            "txid": "e712da809a70f59067c3a65c16f7337079a1113e0072acbef50d96b4af9751a0",
            "outpoint": "e712da809a70f59067c3a65c16f7337079a1113e0072acbef50d96b4af9751a0:0",
            "pkscript": "0014878ff1580d7ceedcd97e1b3cfa7cc0feef2b8f4d",
            "wallet_addr": "bc1qs78lzkqd0nhdekt7rv705lxqlmhjhr6dggcdr4",
            "rune_id": "840000:453",
            "amount": "6666",
            "block_height": 840163,
            "block_timestamp": "2024-04-21T05:48:31.000Z",
            "rune_name": "ORDINALSAREDEAD",
            "spaced_rune_name": "ORDINALS•ARE•DEAD",
            "decimals": 0,
            "sale_info": null
        },
        {
            "event_type": "mint",
            "txid": "82a0b948440e0ba893211fb68805f32ce3f62106a7c688851790769dc8b99ecd",
            "outpoint": null,
            "pkscript": null,
            "wallet_addr": null,
            "rune_id": "840000:453",
            "amount": "6666",
            "block_height": 840163,
            "block_timestamp": "2024-04-21T05:48:31.000Z",
            "rune_name": "ORDINALSAREDEAD",
            "spaced_rune_name": "ORDINALS•ARE•DEAD",
            "decimals": 0,
            "sale_info": null
        },
        ...
    ],
    "block_height": 2585298
}
```
{% endtab %}
{% endtabs %}



## Runes All ID Name Pairs

_<mark style="color:blue;">Included in: Enterprise, Dedicated</mark>_

<mark style="color:blue;">`GET`</mark> `https://api.bestinslot.xyz/v3/runes/all_id_name_pairs`

Returns all runes id-name pairs

<mark style="color:orange;">**NOTE:**</mark> If send\_urls is set to true, we'll also return content and render urls for rune icon. Response will include `render_prefix, render_suffix, content_prefix, content_suffix`  and `r` and `ic` fields in data array. `r` denotes if render is available and urls are constructed using `prefix + ic + suffix`.

Sample query: https://api.bestinslot.xyz/v3/runes/all\_id\_name\_pairs

#### Query Parameters

| Name       | Type     | Description                  |
| ---------- | -------- | ---------------------------- |
| send\_urls | `string` | (optional) "true" or "false" |

**Response**

{% tabs %}
{% tab title="200: OK Success" %}
```json
{
    "data": [
        {
            "i": "840076:2046",
            "n": "HONEYBADGERDONTCARE",
            "sn": "HONEY•BADGER•DONT•CARE"
        },
        {
            "i": "841393:349",
            "n": "BIRDFOURTWOZEROSEVEN",
            "sn": "BIRD•FOUR•TWO•ZERO•SEVEN"
        },
        ...
    ],
    "block_height": 862525
}
```
{% endtab %}
{% endtabs %}



## Runes Historical Prices

_<mark style="color:blue;">Included in: Dedicated</mark>_

<mark style="color:blue;">`GET`</mark> `https://api.bestinslot.xyz/v3/runes/historical_prices`

Returns all historical prices for selected rune

If granularity is set to 1d, it'll return the average price for the day.

Sample query: https://api.bestinslot.xyz/v3/runes/historical\_prices?sort\_by=ts\&order=desc\&offset=0\&count=2000\&rune\_id=1:0

#### Query Parameters

| Name                                       | Type     | Description                        |
| ------------------------------------------ | -------- | ---------------------------------- |
| rune\_name                                 | `string` | (optional) Non-Spaced name of Rune |
| rune\_id                                   | `string` | (optional) Rune ID                 |
| rune\_number                               | `int`    | (optional) Rune Number             |
| sort\_by<mark style="color:red;">\*</mark> | `string` | ts                                 |
| order<mark style="color:red;">\*</mark>    | `string` | asc, desc                          |
| offset<mark style="color:red;">\*</mark>   | `int`    | 0 <= offset                        |
| count<mark style="color:red;">\*</mark>    | `int`    | 20 <= count <= 2000                |
| granularity                                | `string` | (Optional) "1h" or "1d"            |

**NOTE: One of rune\_name, rune\_id or rune\_number must be specified**

**Response**

{% tabs %}
{% tab title="200: OK Success" %}
```json
{
    "data": [
        {
            "timestamp": "2024-09-23T13:00:00.000Z",
            "price": 230.664,
            "volume": 119296
        },
        {
            "timestamp": "2024-09-23T12:00:00.000Z",
            "price": 231.1305896319747,
            "volume": 4266653
        },
        {
            "timestamp": "2024-09-23T11:00:00.000Z",
            "price": 235,
            "volume": 1031318
        },
        {
            "timestamp": "2024-09-23T10:00:00.000Z",
            "price": 235,
            "volume": 2650313
        },
        {
            "timestamp": "2024-09-23T09:00:00.000Z",
            "price": 235,
            "volume": 3747853
        },
        {
            "timestamp": "2024-09-23T08:00:00.000Z",
            "price": 238,
            "volume": 1376502
        },
        {
            "timestamp": "2024-09-23T07:00:00.000Z",
            "price": 238,
            "volume": 5254130
        },
        ...
    ],
    "block_height": 862525
}
```
{% endtab %}
{% endtabs %}
