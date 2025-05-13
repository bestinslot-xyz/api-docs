---
description: Endpoints related to BRC-20 Protocol.
---

# BRC-20

Endpoints' API-Key-Tier availabilities are written for each endpoint.

**To use on testnet4/signet, use your current api-key and send the request to `https://testnet.api.bestinslot.xyz` / `https://signet_api.bestinslot.xyz`**

## BRC-20 Balances of Wallet

_<mark style="color:blue;">Included in: Basic, Pro, Dedicated</mark>_

<mark style="color:blue;">`GET`</mark> `https://api.bestinslot.xyz/v3/brc20/wallet_balances`

Returns BRC-20 token balances of a bitcoin wallet.

Sample query: https://api.bestinslot.xyz/v3/brc20/wallet\_balances?address=bc1pgmtxez2cnp3wk5q52wjcakrkqqfxukgmannrtttm4kq64q53qw7qw44juz

<mark style="color:orange;">**NOTE:**</mark> <mark style="color:orange;"></mark><mark style="color:orange;">min\_listed\_unit\_price is only available on Pro Tier.</mark>

#### Query Parameters

| Name                                      | Type   | Description                                                |
| ----------------------------------------- | ------ | ---------------------------------------------------------- |
| address<mark style="color:red;">\*</mark> | string | bitcoin wallet address                                     |
| ticker                                    | string | (optional) Filter reponse to only show the selected ticker |

{% tabs %}
{% tab title="200: OK Success" %}
```json
{
    "data": [
        {
            "ticker": "oxbt",
            "overall_balance": "5000.0000000000000000",
            "available_balance": "0.000000000000000000000000000000000000",
            "transferrable_balance": "5000.0000000000000000",
            "image_url": null,
            "min_listed_unit_price": 335.94
        },
        {
            "ticker": "mnga",
            "overall_balance": "50000.000000000000",
            "available_balance": "0.000000000000000000000000000000000000",
            "transferrable_balance": "50000.000000000000",
            "image_url": null,
            "min_listed_unit_price": 0.4072
        },
        {
            "ticker": "btoc",
            "overall_balance": "500.0000000000000000",
            "available_balance": "0.000000000000000000000000000000000000",
            "transferrable_balance": "500.0000000000000000",
            "image_url": null,
            "min_listed_unit_price": 144.556
        }
    ],
    "block_height": 795037
}
```
{% endtab %}

{% tab title="429: Too Many Requests Rate limit exceeded" %}

{% endtab %}
{% endtabs %}



## Get BRC-20 Tickers

_<mark style="color:blue;">Included in: Basic, Pro, Dedicated</mark>_

<mark style="color:blue;">`GET`</mark> `https://api.bestinslot.xyz/v3/brc20/tickers`

Returns ordered list of brc-20 tickers with detailed information about them.

Sample query: https://api.bestinslot.xyz/v3/brc20/tickers?sort\_by=remaining\_supply\&order=asc\&offset=0\&count=100\&minting\_status=not\_complete

<mark style="color:orange;">**NOTE:**</mark> <mark style="color:orange;"></mark><mark style="color:orange;">min\_listed\_unit\_price, listed\_supply, marketcap and total\_sale\_info is only available on Pro Tier.</mark>

#### Query Parameters

| Name                                       | Type   | Description                                                                                                                                                                                                                                                                                                 |
| ------------------------------------------ | ------ | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| sort\_by<mark style="color:red;">\*</mark> | string | <p>deploy_ts, max_supply, burned_supply, minted_supply, remaining_supply, holder_count, tx_count, mint_progress<br><br>PRO TIER:<br>min_listed_unit_price, min_listed_unit_price_ordinalswallet, min_listed_unit_price_unisat, min_listed_unit_price_okx, listed_supply, listed_supply_ratio, marketcap</p> |
| order<mark style="color:red;">\*</mark>    | string | asc, desc                                                                                                                                                                                                                                                                                                   |
| offset<mark style="color:red;">\*</mark>   | int    | 0 <= offset                                                                                                                                                                                                                                                                                                 |
| count<mark style="color:red;">\*</mark>    | int    | 20 <= count <= 300                                                                                                                                                                                                                                                                                          |
| minting\_status                            | string | <p>(optional)<br>set to "not_complete" for searching only the tickers with minting_progress&#x3C;100<br><br>set to "completed" for searching only the tickers with minting_progress=100<br><br>do not set to search within all tickers</p>                                                                  |

{% tabs %}
{% tab title="200: OK Success" %}
```json
{
    "data": [
        {
            "ticker": "ordi",
            "original_ticker": "ordi",
            "image_url": "https://bis-brc20.fra1.cdn.digitaloceanspaces.com/big_icons/ORDI.png",
            "decimals": 18,
            "limit_per_mint": 1000,
            "max_supply": 21000000,
            "minted_supply": 21000000,
            "burned_supply": 0,
            "remaining_supply": 0,
            "mint_progress": 100,
            "holder_count": 21425,
            "tx_count": 139415,
            "deploy_ts": "2023-03-08T04:16:31.000Z",
            "deploy_incr_number": 348020,
            "deploy_inscr_id": "b61b0172d95e266c18aea0c624db987e971a5d6d4ebc2aaed85da4642d635735i0",
            "is_self_mint": false,
            "min_listed_unit_price": 66821.445,
            "min_listed_unit_price_ordinalswallet": 71000,
            "min_listed_unit_price_unisat": 66821.445,
            "min_listed_unit_price_okx": 68999.9909090909,
            "listed_supply": 37504.693454911176,
            "listed_supply_ratio": 0.0017859377835671988,
            "marketcap": 1403250345000.0002,
            "total_sale_info": {
                "sale_count": 41894,
                "sale_amount": 6714108,
                "vol_3h": 0,
                "vol_6h": 0,
                "vol_9h": 0,
                "vol_12h": 0,
                "vol_1d": 0,
                "vol_3d": 26836090,
                "vol_7d": 51723223,
                "vol_30d": 1443558529,
                "vol_total": 246425756972
            }
        },
        ...
    ],
    "block_height": 795037
}
```
{% endtab %}

{% tab title="429: Too Many Requests Rate limit exceeded" %}

{% endtab %}
{% endtabs %}



## Get BRC-20 Minting Ticker Count

_<mark style="color:blue;">Included in: Basic, Pro, Dedicated</mark>_

<mark style="color:blue;">`GET`</mark> `https://api.bestinslot.xyz/v3/brc20/ticker_cnt`

Returns the count of brc-20 tickers which haven't finished minting and total brc-20 ticker count.

Sample query: https://api.bestinslot.xyz/v3/brc20/minting\_ticker\_cnt

{% tabs %}
{% tab title="200: OK Success" %}
```json
{
    "data": {
        "minting_ticker_cnt": 29039,
        "ticker_cnt": 36899
    },
    "block_height": 798400
}
```
{% endtab %}

{% tab title="429: Too Many Requests Rate limit exceeded" %}

{% endtab %}
{% endtabs %}



## Get BRC-20 Ticker Information

_<mark style="color:blue;">Included in: Basic, Pro, Dedicated</mark>_

<mark style="color:blue;">`GET`</mark> `https://api.bestinslot.xyz/v3/brc20/ticker_info`

Returns detailed information about a specific BRC-20 ticker.

Sample query: https://api.bestinslot.xyz/v3/brc20/ticker\_info?ticker=ORDI

#### Query Parameters

| Name                                     | Type   | Description   |
| ---------------------------------------- | ------ | ------------- |
| ticker<mark style="color:red;">\*</mark> | string | BRC-20 ticker |

{% tabs %}
{% tab title="200: OK Success" %}
```json
{
    "data": {
        "ticker": "ordi",
        "original_ticker": "ordi",
        "image_url": "https://bis-brc20.fra1.digitaloceanspaces.com/icons/ordi.png",
        "limit_per_mint": 1000,
        "max_supply": 21000000,
        "minted_supply": 21000000,
        "burned_supply": 0,
        "mint_progress": 100,
        "holder_count": 12396,
        "tx_count": 57265,
        "deploy_ts": "2023-03-08T04:16:31.000Z",
        "deploy_incr_number": 348020,
        "deploy_inscr_id": "b61b0172d95e266c18aea0c624db987e971a5d6d4ebc2aaed85da4642d635735i0",
        "is_self_mint": false
    },
    "block_height": 795038
}
```
{% endtab %}

{% tab title="429: Too Many Requests Rate limit exceeded" %}

{% endtab %}
{% endtabs %}



## Get BRC-20 Valid Transfer Notes

_<mark style="color:blue;">Included in: Basic, Pro, Dedicated</mark>_

<mark style="color:blue;">`GET`</mark> `https://api.bestinslot.xyz/v3/brc20/validtxnotes`

Returns ordered list of brc-20 valid transfer notes of a given ticker with detailed information about them.

Sample query: https://api.bestinslot.xyz/v3/brc20/validtxnotes?ticker=ordi\&sort\_by=min\_unit\_price\&order=asc\&offset=0\&count=100

#### Query Parameters

| Name                                       | Type   | Description                                                |
| ------------------------------------------ | ------ | ---------------------------------------------------------- |
| sort\_by<mark style="color:red;">\*</mark> | string | inscr\_num, min\_price, min\_unit\_price, transfer\_amount |
| order<mark style="color:red;">\*</mark>    | string | asc, desc                                                  |
| offset<mark style="color:red;">\*</mark>   | int    | 0 <= offset                                                |
| count<mark style="color:red;">\*</mark>    | int    | 20 <= count <= 2000                                        |
| ticker<mark style="color:red;">\*</mark>   | string | BRC-20 ticker                                              |

{% tabs %}
{% tab title="200: OK Success" %}
```json
{
    "data": [
        {
            "inscription_id": "b82f206d2d1bd7e5a2752f969acf63ac3664b2016872a4cbcc1d81a06da0bb34i0",
            "inscription_number": 27576503,
            "transfer_amount": "1000.0000000000000000",
            "is_valid": true,
            "is_used": false,
            "satpoint": "b82f206d2d1bd7e5a2752f969acf63ac3664b2016872a4cbcc1d81a06da0bb34:0:0",
            "min_price": 15575400,
            "min_unit_price": "15575.4000000000000000",
            "ordinalswallet_price": null,
            "ordinalswallet_unit_price": null,
            "okx_price": null,
            "okx_unit_price": null,
            "unisat_price": 15575400,
            "unisat_unit_price": "15575.4000000000000000"
        },
        ...
    ],
    "block_height": 798387
}
```
{% endtab %}

{% tab title="429: Too Many Requests Rate limit exceeded" %}

{% endtab %}
{% endtabs %}



## Get BRC-20 Valid Transfer Notes of a Wallet

_<mark style="color:blue;">Included in: Basic, Pro, Dedicated</mark>_

<mark style="color:blue;">`GET`</mark> `https://api.bestinslot.xyz/v3/brc20/validtxnotes_wallet`

Returns ordered list of brc-20 valid transfer notes of a given BTC wallet with detailed information about them.

Sample query: https://api.bestinslot.xyz/v3/brc20/validtxnotes\_wallet?address=bc1pgmtxez2cnp3wk5q52wjcakrkqqfxukgmannrtttm4kq64q53qw7qw44juz\&sort\_by=min\_unit\_price\&order=asc\&offset=0\&count=100

#### Query Parameters

| Name                                       | Type   | Description                                                |
| ------------------------------------------ | ------ | ---------------------------------------------------------- |
| sort\_by<mark style="color:red;">\*</mark> | string | inscr\_num, min\_price, min\_unit\_price, transfer\_amount |
| order<mark style="color:red;">\*</mark>    | string | asc, desc                                                  |
| offset<mark style="color:red;">\*</mark>   | int    | 0 <= offset                                                |
| count<mark style="color:red;">\*</mark>    | int    | 20 <= count <= 2000                                        |
| address<mark style="color:red;">\*</mark>  | string | bitcoin wallet address                                     |

{% tabs %}
{% tab title="200: OK Success" %}
```json
{
    "data": [
        {
            "inscription_id": "c229a89b9f2e9fb6fd5ef124e6dcf4394163b5ff518f1c5d5ad62eaa02a61c56i0",
            "inscription_number": 10509196,
            "ticker": "giga",
            "transfer_amount": "1900000.000000000000",
            "is_valid": true,
            "is_used": false,
            "satpoint": "c229a89b9f2e9fb6fd5ef124e6dcf4394163b5ff518f1c5d5ad62eaa02a61c56:0:0",
            "min_price": 326880,
            "min_unit_price": "0.17204200000000000000",
            "ordinalswallet_price": null,
            "ordinalswallet_unit_price": null,
            "okx_price": null,
            "okx_unit_price": null,
            "unisat_price": 326880,
            "unisat_unit_price": "0.17204200000000000000"
        },
        ...
    ],
    "block_height": 798387
}
```
{% endtab %}

{% tab title="429: Too Many Requests Rate limit exceeded" %}

{% endtab %}
{% endtabs %}



## BRC-20 Validity Check

_<mark style="color:blue;">Included in: Basic, Pro, Dedicated</mark>_

<mark style="color:blue;">`GET`</mark> `https://api.bestinslot.xyz/v3/brc20/single_info`

Returns validity details about a specific inscription.

Sample query: https://api.bestinslot.xyz/v3/brc20/single\_info?inscription\_id=859905a264deaab7ce88832ad73684ddc45cf9e0022e2700b8ac549f14199279i0

#### Query Parameters

| Name                                              | Type   | Description    |
| ------------------------------------------------- | ------ | -------------- |
| inscription\_id<mark style="color:red;">\*</mark> | string | inscription id |

{% tabs %}
{% tab title="200: OK Success" %}
```json
{
    "data": {
        "transfer_info": {
            "is_valid": true,
            "ticker": "ordi",
            "original_ticker": "ordi",
            "amount": "100.0000000000000000",
            "is_used": true
        },
        "mint_info": {
            "is_valid": false,
            "ticker": null,
            "original_ticker": null,
            "amount": null,
            "mint_wallet": null,
            "parent_id": null
        },
        "deploy_info": {
            "is_valid": false,
            "ticker": null,
            "original_ticker": null,
            "max_supply": null,
            "decimals": null,
            "limit_per_mint": null,
            "is_self_mint": null
        }
    },
    "block_height": 795034
}
```
{% endtab %}

{% tab title="429: Too Many Requests Rate limit exceeded" %}

{% endtab %}
{% endtabs %}



## BRC-20 Batch Validity Check

_<mark style="color:blue;">Included in: Basic, Pro, Dedicated</mark>_

<mark style="color:green;">`POST`</mark> `https://api.bestinslot.xyz/v3/brc20/batch_info`

Returns validity details about a specific inscription.

Sample query: \
url: \
`https://api.bestinslot.xyz/v3/brc20/batch_info`

data: \
`{ "queries": [ "859905a264deaab7ce88832ad73684ddc45cf9e0022e2700b8ac549f14199279i0", "62a2e184ae03ef3ca20a92b628b45b644147fad3e0b1de096f511d41bfcb32bai0", "b61b0172d95e266c18aea0c624db987e971a5d6d4ebc2aaed85da4642d635735i0" ] }`

headers: \
`{ "Content-Type":"application/json", "x-api-key":"...." }`

#### Request Body

| Name                                      | Type  | Description                                               |
| ----------------------------------------- | ----- | --------------------------------------------------------- |
| queries<mark style="color:red;">\*</mark> | Array | <p>Array of inscription id strings<br>Max length: 100</p> |

{% tabs %}
{% tab title="200: OK Success" %}
```json
{
    "data": [
        {
            "inscription_id": "859905a264deaab7ce88832ad73684ddc45cf9e0022e2700b8ac549f14199279i0",
            "transfer_info": {
                "is_valid": true,
                "ticker": "ordi",
                "original_ticker": "ordi",
                "amount": "100.000000000000000000",
                "is_used": true
            },
            "mint_info": {
                "is_valid": false,
                "ticker": null,
                "original_ticker": null,
                "amount": null,
                "mint_wallet": null,
                "parent_id": null
            },
            "deploy_info": {
                "is_valid": false,
                "ticker": null,
                "original_ticker": null,
                "max_supply": null,
                "decimals": null,
                "limit_per_mint": null,
                "is_self_mint": null
            }
        },
        {
            "inscription_id": "62a2e184ae03ef3ca20a92b628b45b644147fad3e0b1de096f511d41bfcb32bai0",
            "transfer_info": {
                "is_valid": false,
                "ticker": null,
                "original_ticker": null,
                "amount": null,
                "is_used": null
            },
            "mint_info": {
                "is_valid": false,
                "ticker": null,
                "original_ticker": null,
                "amount": null,
                "mint_wallet": null,
                "parent_id": null
            },
            "deploy_info": {
                "is_valid": true,
                "ticker": "zeee",
                "original_ticker": "zeee",
                "max_supply": "0.000000000000000001",
                "decimals": "18",
                "limit_per_mint": "1",
                "is_self_mint": false
            }
        },
        {
            "inscription_id": "b61b0172d95e266c18aea0c624db987e971a5d6d4ebc2aaed85da4642d635735i0",
            "transfer_info": {
                "is_valid": false,
                "ticker": null,
                "original_ticker": null,
                "amount": null,
                "is_used": null
            },
            "mint_info": {
                "is_valid": false,
                "ticker": null,
                "original_ticker": null,
                "amount": null,
                "mint_wallet": null,
                "parent_id": null
            },
            "deploy_info": {
                "is_valid": true,
                "ticker": "ordi",
                "original_ticker": "ordi",
                "max_supply": "21000000.000000000000000000",
                "decimals": "18",
                "limit_per_mint": "1000000000000000000000",
                "is_self_mint": false
            }
        }
    ],
    "block_height": 821920
}
```
{% endtab %}

{% tab title="429: Too Many Requests Rate limit exceeded" %}

{% endtab %}
{% endtabs %}



## Get BRC-20 Ticker Holders

_<mark style="color:blue;">Included in: Basic, Pro, Dedicated</mark>_

<mark style="color:blue;">`GET`</mark> `https://api.bestinslot.xyz/v3/brc20/holders`

Returns ordered list of brc-20 holders and their balances.

Sample query: https://api.bestinslot.xyz/v3/brc20/holders?ticker=ordi\&sort\_by=balance\&order=desc\&offset=10000\&count=500

#### Query Parameters

| Name                                       | Type   | Description        |
| ------------------------------------------ | ------ | ------------------ |
| sort\_by<mark style="color:red;">\*</mark> | string | balance            |
| order<mark style="color:red;">\*</mark>    | string | asc, desc          |
| offset<mark style="color:red;">\*</mark>   | int    | 0 <= offset        |
| count<mark style="color:red;">\*</mark>    | int    | 20 <= count <= 500 |
| ticker<mark style="color:red;">\*</mark>   | string | BRC-20 ticker      |

{% tabs %}
{% tab title="200: OK Success" %}
```json
{
    "data": [
        {
            "pkscript": "51207fee8ce58498d8f5228a1f848d9a5d3cf0a8918dbe54935c858875ed23814523",
            "wallet": "bc1p0lhgeevynrv02g52r7zgmxja8nc23yvdhe2fxhy93p676gupg53sw46fy3",
            "overall_balance": "10.0000000000000000"
        },
        ...
    ],
    "block_height": 795034
}
```
{% endtab %}

{% tab title="429: Too Many Requests Rate limit exceeded" %}

{% endtab %}
{% endtabs %}



## Get BRC-20 Event from TxId

_<mark style="color:blue;">Included in: Basic, Pro, Dedicated</mark>_

<mark style="color:blue;">`GET`</mark> `https://api.bestinslot.xyz/v3/brc20/event_from_txid`

Returns BRC-20 events in a given bitcoin txid.

Sample query: https://api.bestinslot.xyz/v3/brc20/event\_from\_txid?txid=21b7b3bf48b04af8102a560acdbf3993411a96caa9327b6c07423096ec2e17da

<mark style="color:orange;">NOTE: price and marketplace\_type information is only available in PRO Tier.</mark>

#### Query Parameters

| Name                                   | Type   | Description  |
| -------------------------------------- | ------ | ------------ |
| txid<mark style="color:red;">\*</mark> | string | Bitcoin txid |

{% tabs %}
{% tab title="200: OK Success" %}
```json
{
    "data": [
        {
            "inscription_id": "6d4a1438ab43f941db9671fe8c4e5566984e14f0545f97143fa4df397295b755i0",
            "event_type": "transfer-transfer",
            "event": {
                "tick": "𝛑",
                "amount": "31415926535000000000000000000",
                "using_tx_id": "60998008",
                "spent_wallet": "bc1q7jyhzrgmaw26sggejpc5fe0ghecc53lu06u28c",
                "source_wallet": "bc1qgzdxs7vtzj3xywa9g50kdjkhsxqlu8ce6h6c63",
                "spent_pkScript": "0014f489710d1beb95a82119907144e5e8be718a47fc",
                "source_pkScript": "0014409a68798b14a2623ba5451f66cad78181fe1f19",
                "price": 530300,
                "marketplace_type": "okx"
            }
        }
    ],
    "block_height": 824865
}
```
{% endtab %}

{% tab title="429: Too Many Requests Rate limit exceeded" %}

{% endtab %}

{% tab title="403: Forbidden Invalid API-Key" %}

{% endtab %}
{% endtabs %}



## Get BRC-20 Sales Information

_<mark style="color:blue;">Included in: Pro, Dedicated</mark>_

<mark style="color:blue;">`GET`</mark> `https://api.bestinslot.xyz/v3/brc20/sales_info`

Returns sales and volume information about a specific brc-20 ticker.

Sample query: https://api.bestinslot.xyz/v3/brc20/sales\_info?ticker=ordi\&marketplace\_type=magiceden

#### Query Parameters

| Name                                     | Type   | Description                                                                                                 |
| ---------------------------------------- | ------ | ----------------------------------------------------------------------------------------------------------- |
| ticker<mark style="color:red;">\*</mark> | string | BRC-20 ticker                                                                                               |
| marketplace\_type                        | string | Optional parameter to filter only by a given marketplace. You can find the allowed types on Constants Page. |

{% tabs %}
{% tab title="200: OK Success" %}
```json
{
    "data": {
        "marketplace": "all",
        "vol_3h": 0,
        "vol_6h": 4855500,
        "vol_9h": 5266074,
        "vol_12h": 5266074,
        "vol_1d": 112874701,
        "vol_3d": 171112507,
        "vol_7d": 230695357,
        "vol_30d": 777270095,
        "vol_total": 139743502715,
        "sale_count": 23843, // how many sales have happened
        "sale_amount": 5120986 // the total amount of tokens sold
    },
    "block_height": 805713
}
```
{% endtab %}

{% tab title="429: Too Many Requests Rate limit exceeded" %}

{% endtab %}

{% tab title="403: Forbidden Invalid API-Key" %}

{% endtab %}
{% endtabs %}



## Get BRC-20 Market Information

_<mark style="color:blue;">Included in: Pro, Dedicated</mark>_

<mark style="color:blue;">`GET`</mark> `https://api.bestinslot.xyz/v3/brc20/market_info`

Returns market information like marketcap, listed count, floor price about a specific BRC-20 ticker.

Sample query: https://api.bestinslot.xyz/v3/brc20/market\_info?ticker=ordi

#### Query Parameters

| Name                                     | Type   | Description   |
| ---------------------------------------- | ------ | ------------- |
| ticker<mark style="color:red;">\*</mark> | string | BRC-20 ticker |

{% tabs %}
{% tab title="200: OK Success" %}
```json
{
    "data": {
        "marketcap": 1403250345000.0002,
        "min_listed_unit_price": 66821.445,
        "min_listed_unit_price_ordinalswallet": 71000,
        "min_listed_unit_price_unisat": 66821.445,
        "min_listed_unit_price_okx": 68999.9909090909,
        "listed_supply": 37504.693454911176,
        "listed_supply_ratio": 0.0017859377835671988
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



## Get BRC-20 Listings

_<mark style="color:blue;">Included in: Pro, Dedicated</mark>_

<mark style="color:blue;">`GET`</mark> `https://api.bestinslot.xyz/v3/brc20/listings`

Returns ordered list of listings of a specific BRC-20 ticker.

Sample query: https://api.bestinslot.xyz/v3/brc20/listings?ticker=ordi\&sort\_by=min\_unit\_price\&order=desc\&offset=0\&count=100

#### Query Parameters

| Name                                       | Type   | Description                                                                                                                                         |
| ------------------------------------------ | ------ | --------------------------------------------------------------------------------------------------------------------------------------------------- |
| sort\_by<mark style="color:red;">\*</mark> | string | <p>min_price, min_unit_price, ordinalswallet_price, ordinalswallet_unit_price, unisat_price, unisat_unit_price,<br>okx_price,<br>okx_unit_price</p> |
| order<mark style="color:red;">\*</mark>    | string | asc, desc                                                                                                                                           |
| offset<mark style="color:red;">\*</mark>   | int    | 0 <= offset <= 5k                                                                                                                                   |
| count<mark style="color:red;">\*</mark>    | int    | 20 <= count <= 100                                                                                                                                  |
| ticker<mark style="color:red;">\*</mark>   | string | BRC-20 ticker                                                                                                                                       |

{% tabs %}
{% tab title="200: OK Success" %}
```json
{
    "data": [
        {
            "inscription_id": "6d6bdc8a1c36f80144ce250745840ab10e1308a4b8cc9a769d3719095e1242e7i0",
            "transfer_amount": "1.00000000000000000000",
            "min_price": 300000000,
            "min_unit_price": "300000000.00000000000000000000",
            "ordinalswallet_price": 300000000,
            "ordinalswallet_unit_price": "300000000.00000000000000000000",
            "unisat_price": null,
            "unisat_unit_price": null,
            "okx_price": null,
            "okx_unit_price": null,
            "owner_wallet_addr": "bc1p96u7df3xhr6x5h8ch9dld5le73k820awhhu6fpnn0r3k6xprz6tqtw2h2u"
        },
        ...
    ],
    "block_height": 795034
}
```
{% endtab %}

{% tab title="429: Too Many Requests Rate limit exceeded" %}

{% endtab %}

{% tab title="403: Forbidden Invalid API-Key" %}

{% endtab %}
{% endtabs %}



## Get BRC-20 Activity

_<mark style="color:blue;">Included in: Pro, Dedicated</mark>_

<mark style="color:blue;">`GET`</mark> `https://api.bestinslot.xyz/v3/brc20/activity`

Returns ordered list of inscribes, sales and transfers of a specific BRC-20 ticker.

<mark style="color:orange;">NOTE: Use last\_new\_satpoint to continue fetching the activity from where you've left off. new\_satpoint uniquely addresses a single inscription transfer, so by setting order to asc, and last\_new\_satpoint to the latest new\_satpoint value that you've received, you can retrieve the new activities.</mark>

Sample query: https://api.bestinslot.xyz/v3/brc20/activity?ticker=ordi\&activity\_filter=7\&sort\_by=ts\&order=desc\&offset=1000\&count=100\&last\_new\_satpoint=a47f806f7fa622a44bc77bc886c8e0646cc61878d412285aa4a297cf2a5ce296:0:0

#### Query Parameters

| Name                                               | Type   | Description                                                                                                             |
| -------------------------------------------------- | ------ | ----------------------------------------------------------------------------------------------------------------------- |
| sort\_by<mark style="color:red;">\*</mark>         | string | ts, unit\_price, amount, sale\_price                                                                                    |
| order<mark style="color:red;">\*</mark>            | string | asc, desc                                                                                                               |
| offset<mark style="color:red;">\*</mark>           | int    | 0 <= offset <= 5k                                                                                                       |
| count<mark style="color:red;">\*</mark>            | int    | 20 <= count <= 100                                                                                                      |
| ticker<mark style="color:red;">\*</mark>           | string | BRC-20 ticker                                                                                                           |
| activity\_filter<mark style="color:red;">\*</mark> | int    | <p>1 -> mints<br>2 -> transfers<br>4 -> sales<br>combine with or operator (e.g. sold &#x26; transferred: 2 | 4 = 6)</p> |
| last\_new\_satpoint                                | string | (optional) use this with offset 0 to continue from a known transfer                                                     |
| wallet                                             | string | (optional) bitcoin wallet filter                                                                                        |

{% tabs %}
{% tab title="200: OK Success" %}
```json
{
    "data": [
        {
            "_tx_id": 15271002,
            "inscription_id": "5f236832ad63e35d005f93e14ce93741836732599efc921ab074e079b36ea418i0",
            "amount": "100.0000000000000000",
            "sale_price": -1,
            "unit_price": "-0.01000000000000000000",
            "activity_type": 1,
            "from_wallet": "bc1q3sda3q9hd82qzm8j9wfff0afmdkvsh8qafmrfh",
            "to_wallet": "1P3XJT34R9bVntfQXVoZDwA6z4oxjaaiTU",
            "block_height": 795034,
            "ts": "2023-06-19T09:30:18.000Z",
            "new_satpoint": "a47f806f7fa622a44bc77bc886c8e0646cc61878d412285aa4a297cf2a5ce296:0:0",
            "tx_id": "a47f806f7fa622a44bc77bc886c8e0646cc61878d412285aa4a297cf2a5ce296"
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



## Get BRC-20 Wallet Activity

_<mark style="color:blue;">Included in: Pro, Dedicated</mark>_

<mark style="color:blue;">`GET`</mark> `https://api.bestinslot.xyz/v3/brc20/wallet_activity`

Returns ordered list of deploy-inscribe, mint-inscribe, transfer-inscribe and transfer-transfer of a given bitcoin wallet.

Sample query: https://api.bestinslot.xyz/v3/brc20/wallet\_activity?order=asc\&offset=0\&count=2000\&wallet\_addr=bc1pxaneaf3w4d27hl2y93fuft2xk6m4u3wc4rafevc6slgd7f5tq2dqyfgy06

#### Query Parameters

| Name                                           | Type   | Description                      |
| ---------------------------------------------- | ------ | -------------------------------- |
| order<mark style="color:red;">\*</mark>        | string | asc, desc (ordered by timestamp) |
| offset<mark style="color:red;">\*</mark>       | int    | 0 <= offset <= 5k                |
| count<mark style="color:red;">\*</mark>        | int    | 20 <= count <= 2000              |
| wallet\_addr<mark style="color:red;">\*</mark> | string | bitcoin wallet address           |

{% tabs %}
{% tab title="200: OK Success" %}
```json
{
    "data": [
        {
            "ticker": "ordi",
            "event_type": "deploy-inscribe",
            "to_wallet": "bc1pxaneaf3w4d27hl2y93fuft2xk6m4u3wc4rafevc6slgd7f5tq2dqyfgy06",
            "block_height": 779832,
            "ts": "2023-03-08T04:16:31.000Z",
            "inscription_id": "b61b0172d95e266c18aea0c624db987e971a5d6d4ebc2aaed85da4642d635735i0",
            "sale_price": null,
            "unit_price": null,
            "amount": null
        },
        ...
    ],
    "block_height": 844736
}
```
{% endtab %}
{% endtabs %}



## Get BRC-20 Activity on Block

_<mark style="color:blue;">Included in: Enterprise, Dedicated with Enterprise Endpoints</mark>_

<mark style="color:blue;">`GET`</mark> `https://api.bestinslot.xyz/v3/brc20/activity_on_block`

Returns ordered list of mint note and transfer note inscribes, and transfer note transfers in a given block height.

<mark style="color:orange;">NOTE: block\_height at the response is not the queried block height. It is the final indexed block height of our indexer.</mark>

Sample query: https://api.bestinslot.xyz/v3/brc20/activity\_on\_block?block\_height=802396

#### Query Parameters

| Name                                            | Type | Description                                                                 |
| ----------------------------------------------- | ---- | --------------------------------------------------------------------------- |
| block\_height<mark style="color:red;">\*</mark> | int  | block height, must be smaller than or equal to current bitcoin block height |

{% tabs %}
{% tab title="200: OK Success" %}
```json
{
    "data": [
        {
            "id": 28093931,
            "inscription_id": "6d5ba7f257f634ee7ec3220263dc3c5c6df13e6d5f3f61957250ceed1c43666ai0",
            "old_pkscript": "0014870dba15d6b5a0563b6df472359a7ef75d21f26c",
            "old_wallet": "bc1qsuxm59wkkks9vwmd73ertxn77awjrunv8x0nv6",
            "old_satpoint": "6d5ba7f257f634ee7ec3220263dc3c5c6df13e6d5f3f61957250ceed1c43666a:0:0",
            "new_pkscript": "0014ad42179475826f3cae94c1c3bae2797c6933a53a",
            "new_wallet": "bc1q44pp09r4sfhnet55c8pm4cne035n8ff6t0lhgz",
            "new_satpoint": "da30e16bda726bee66f94d2872a90350c29b08bca01ad8070e4ccb06112a0b8a:1:0",
            "tick": "rdex",
            "original_tick": "rdex",
            "amount": "10000000000000000000000",
            "activity_type": "transfer-transfer"
        },
        {
            "id": 28093932,
            "inscription_id": "8e9b5a1c8c18d420a37bcc95599883daaadd351990e2156318c6d61d2669d773i0",
            "old_pkscript": "",
            "old_wallet": "",
            "old_satpoint": "",
            "new_pkscript": "a914d9f616912c258bbaff7c0f02e3915bdebf39533e87",
            "new_wallet": "3MZVMg8qC42cBhfczWWRr9jds1rP2kqmJ8",
            "new_satpoint": "8e9b5a1c8c18d420a37bcc95599883daaadd351990e2156318c6d61d2669d773:0:0",
            "tick": "bank",
            "original_tick": "bank",
            "amount": "880079000000000000000000",
            "activity_type": "transfer-inscribe"
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



## Get BRC-20 Balance on Block

_<mark style="color:blue;">Included in: Enterprise, Dedicated with Enterprise Endpoints</mark>_

<mark style="color:blue;">`GET`</mark> `https://api.bestinslot.xyz/v3/brc20/balance_on_block`

Returns BRC-20 balances of a given wallet (address or pkscript(scriptPubKey)) at the **beginning of** the given block height.

<mark style="color:orange;">NOTE: block\_height at the response is not the queried block height. It is the final indexed block height of our indexer.</mark>

Sample query: https://api.bestinslot.xyz/v3/brc20/balance\_on\_block?block\_height=802397\&pkscript=0014cd6cccc69331a96ea0fe0fa5d1d184a811979a8b

#### Query Parameters

| Name                                            | Type   | Description                                                                          |
| ----------------------------------------------- | ------ | ------------------------------------------------------------------------------------ |
| block\_height<mark style="color:red;">\*</mark> | int    | block height, must not be bigger than (current bitcoin block height + 1)             |
| pkscript                                        | string | scriptPubKey of the wallet. Only one of the wallet/pkscipt parameters should be set! |
| wallet                                          | string | address of the wallet. Only one of the wallet/pkscipt parameters should be set!      |

{% tabs %}
{% tab title="200: OK Success" %}
```json
{
    "data": [
        {
            "tick": "bili",
            "balance": "1000000000000000000"
        },
        {
            "tick": "𝜋",
            "balance": "3141592653589793238"
        },
        {
            "tick": "🌞",
            "balance": "5000000000000000000"
        },
        {
            "tick": "🦎",
            "balance": "10000000000000000000"
        },
        {
            "tick": "rcsv",
            "balance": "20000000000000000000"
        },
        {
            "tick": "🦓",
            "balance": "21000000000000000000"
        },
        {
            "tick": "cncl",
            "balance": "48000000000000000000"
        },
        {
            "tick": "🌚",
            "balance": "50000000000000000000"
        },
        {
            "tick": "🤑",
            "balance": "100000000000000000000"
        },
        {
            "tick": "🜚",
            "balance": "267000000000000000000"
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



## Get BRC-20 Balance on Block Batch

_<mark style="color:blue;">Included in: Enterprise, Dedicated with Enterprise Endpoints</mark>_

<mark style="color:green;">`POST`</mark> `https://api.bestinslot.xyz/v3/brc20/batch_balance_on_block`

Returns BRC-20 ticker balance of several given wallet (address or pkscript(scriptPubKey)) at the **beginning of** the given block height.

Query limit is **100** per request.

<mark style="color:orange;">NOTE: block\_height at the response is not the queried block height. It is the final indexed block height of our indexer.</mark>

<mark style="color:orange;">NOTE: if the queried block hasn't been indexed yet, it'll return</mark> <mark style="color:orange;"></mark><mark style="color:orange;">`{error: "block not indexed yet"}`</mark> <mark style="color:orange;"></mark><mark style="color:orange;">in response.</mark>

Sample query: \
url: \
`https://api.bestinslot.xyz/v3/brc20/batch_balance_on_block`

data: \
`{"queries":[{"pkscript":"0014cd6cccc69331a96ea0fe0fa5d1d184a811979a8b","block_height":802397,"ticker":"pepe"},{"pkscript":"512037679ea62eab55ebfd442c53c4ad46b6b75e45d8a8fa9cb31a87d0df268b029a","block_height":802397,"ticker":"meme"}]}`

headers: \
`{ "Content-Type":"application/json", "x-api-key":"...." }`

#### Request Body

| Name                                      | Type       | Description                                                                                                             |
| ----------------------------------------- | ---------- | ----------------------------------------------------------------------------------------------------------------------- |
| queries<mark style="color:red;">\*</mark> | JSON Array | List of (block\_height, ticker, (wallet\|pkscript)) objects. (only one of wallet / pkscript is required for each query) |

{% tabs %}
{% tab title="200: OK Success" %}
```json
{
    "data": [
        {
            "block_height": 802397,
            "tick": "pepe",
            "balance": "11500000000000000000000",
            "pkscript": "0014cd6cccc69331a96ea0fe0fa5d1d184a811979a8b"
        },
        {
            "block_height": 802397,
            "tick": "meme",
            "balance": "1000000000000000000",
            "pkscript": "512037679ea62eab55ebfd442c53c4ad46b6b75e45d8a8fa9cb31a87d0df268b029a"
        }
    ],
    "block_height": 814812
}
```
{% endtab %}

{% tab title="429: Too Many Requests Rate limit exceeded" %}

{% endtab %}

{% tab title="403: Forbidden Invalid API-Key" %}

{% endtab %}
{% endtabs %}



## Get BRC-20 All Valid Tx Notes

_<mark style="color:blue;">Included in: Enterprise, Dedicated with Enterprise Endpoints</mark>_

<mark style="color:blue;">`GET`</mark> `https://api.bestinslot.xyz/v3/brc20/all_validtxnotes`

Returns **All** valid BRC-20 tx notes.

Sample query: https://api.bestinslot.xyz/v3/brc20/all\_validtxnotes

{% tabs %}
{% tab title="200: OK Success" %}
```json
{
    "data": [
        {
            "inscription_id": "1c0c902e49a9730671069c0b273ecf880c9d173a6716ef358d7323703902d71di0",
            "ticker": "drac",
            "amount": "21040000000000000000000",
            "source_pkscript": "5120df3a840ed1ea279110180fd09853e5b15a162c53309162dae0b8aa10b7b2919a"
        },
        ...
    ],
    "block_height": 814029
}
```
{% endtab %}

{% tab title="429: Too Many Requests Rate limit exceeded" %}

{% endtab %}

{% tab title="403: Forbidden Invalid API-Key" %}

{% endtab %}
{% endtabs %}



## Get BRC-20 All Balances

_<mark style="color:blue;">Included in: Enterprise, Dedicated with Enterprise Endpoints</mark>_

<mark style="color:blue;">`GET`</mark> `https://api.bestinslot.xyz/v3/brc20/all_balances`

Returns **All** BRC-20 balances of all wallets.

Sample query: https://api.bestinslot.xyz/v3/brc20/all\_balances

{% tabs %}
{% tab title="200: OK Success" %}
```json
{
    "data": [
        {
            "wallet": "bc1qqqpx5690calxc5q2x83mhyftk6zmtvlprvdujz",
            "pkscript": "001400026a68afc77e6c500a31e3bb912bb685b5b3e1",
            "tick": "btcs",
            "overall_balance": "10.0000000000000000",
            "available_balance": "10.0000000000000000"
        },
        ...
    ],
    "block_height": 814029
}
```
{% endtab %}

{% tab title="429: Too Many Requests Rate limit exceeded" %}

{% endtab %}

{% tab title="403: Forbidden Invalid API-Key" %}

{% endtab %}
{% endtabs %}
