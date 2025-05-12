---
description: Endpoints related to Bitcoin Wallets.
---

# Wallets

Endpoints' API-Key-Tier availabilities are written for each endpoint.

**To use on testnet4/signet, use your current api-key and send the request to `https://testnet.api.bestinslot.xyz` / `https://signet_api.bestinslot.xyz`**

## BTC Testnet4 Faucet (only on testnet)

_<mark style="color:blue;">Included in: Basic, Pro, Dedicated</mark>_

<mark style="color:blue;">`GET`</mark> `https://testnet.api.bestinslot.xyz/v3/wallet/testnet_faucet`

A testnet BTC faucet that mints 0.01 tBTC to target address.

**NOTE: Limited with 10 request per 24 hours per key.**

Sample query: https://testnet.api.bestinslot.xyz/v3/wallet/testnet\_faucet?address=tb1p9ts4eu2s4adgjwumdmcu9qfw0hcavrh8m54tyrd39lkk7h4940yq2dmvzx

#### Query Parameters

| Name                                      | Type     | Description                    |
| ----------------------------------------- | -------- | ------------------------------ |
| address<mark style="color:red;">\*</mark> | `string` | Testnet Bitcoin wallet address |

**Response**

{% tabs %}
{% tab title="200: OK Success" %}
```json
{
    "transfer_txid": "d32bb47c7728dbe89289694a54827ecabd8052a5e6c1475ac5a126986e79be1b"
}
```
{% endtab %}
{% endtabs %}



## Get Wallet Inscriptions

_<mark style="color:blue;">Included in: Basic, Pro, Dedicated</mark>_

<mark style="color:blue;">`GET`</mark> `https://api.bestinslot.xyz/v3/wallet/inscriptions`

Returns ordered list of inscriptions of a wallet.

Sample query: https://api.bestinslot.xyz/v3/wallet/inscriptions?address=bc1p9ckplx7pesuh396he7nk0qzxrhyewd2ytrz9s2444dkl2c8gerdsrq7xjd\&sort\_by=inscr\_num\&order=desc\&offset=0\&count=2000\&exclude\_brc20=true\&cursed\_only=true

<mark style="color:orange;">**NOTE:**</mark> <mark style="color:orange;"></mark><mark style="color:orange;">last\_sale\_price is only available on Pro Tier.</mark>

#### Query Parameters

| Name                                       | Type   | Description                                               |
| ------------------------------------------ | ------ | --------------------------------------------------------- |
| sort\_by<mark style="color:red;">\*</mark> | string | inscr\_num                                                |
| order<mark style="color:red;">\*</mark>    | string | asc, desc                                                 |
| offset<mark style="color:red;">\*</mark>   | int    | 0 <= offset                                               |
| count<mark style="color:red;">\*</mark>    | int    | 20 <= count <= 2000                                       |
| address<mark style="color:red;">\*</mark>  | string | bitcoin wallet address                                    |
| exclude\_brc20                             | bool   | (optional) set to true to exclude brc-20 inscriptions     |
| cursed\_only                               | bool   | (optional) set to true to return only cursed inscriptions |
| collection\_slug                           | string | (optional) filter by collection slug                      |

{% tabs %}
{% tab title="200: OK Success" %}
```json
{
    "data": [
        {
            "inscription_name": "Runestone",
            "inscription_id": "c1731231b40c1bf0a7d5c06659067f276e6d4db2980bdc29f18938c7dbfd256ai1135",
            "inscription_number": 64542114,
            "parent_ids": [
                "fdb2df5d2b16db1ebcbf09e2d23b3f4e417db44b58e712c99b61f26b52c7cbb5i0"
            ],
            "output_value": 330,
            "genesis_block_hash": "000000000000000000018ddf8a6484db391fb85c9f9ddc384f03a92729423aaf",
            "genesis_ts": "2024-04-13T04:25:01.000Z",
            "metadata": {
                "name": "Runestone"
            },
            "owner_wallet_addr": "bc1pp5xk5dxklrfxk4yzdkel09yeqqczk5s3425zg9fj6p8qpm8axdes94yhu7",
            "mime_type": "model/gltf+json",
            "last_sale_price": 3950000,
            "slug": "runestone",
            "collection_name": "Runestone",
            "satpoint": "b5567d810d09a61a373f8cbec32322a4c42aa5ff2c163d5eb284aa52c9a0ffff:7:0",
            "last_transfer_block_height": 836794,
            "genesis_height": 834864,
            "content_url": "https://bis-ord-content.fra1.cdn.digitaloceanspaces.com/ordinals/c1731231b40c1bf0a7d5c06659067f276e6d4db2980bdc29f18938c7dbfd256ai1135",
            "bis_url": "https://bestinslot.xyz/ordinals/inscription/c1731231b40c1bf0a7d5c06659067f276e6d4db2980bdc29f18938c7dbfd256ai1135",
            "render_url": null,
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
    "block_height": 795034
}
```
{% endtab %}

{% tab title="429: Too Many Requests Rate limit exceeded" %}

{% endtab %}
{% endtabs %}



## Get Batch Wallet Inscriptions

_<mark style="color:blue;">Included in: Pro, Dedicated</mark>_

<mark style="color:green;">`POST`</mark> `https://api.bestinslot.xyz/v3/wallet/inscriptions_batch`

Returns ordered list of inscriptions of given wallets (up to 100 wallet).

Sample query: \
url: https://api.bestinslot.xyz/v3/wallet/inscriptions\_batch\
data: {"addresses":\["bc1pfxhh3yh5pp4s8pf6wjthe5dwsl6nva04n8zdsw4wsnq76kpy2fsqxgse5d","bc1psrvymaz9gx4ljw0x4lpsscrsh2xy8u4yx0ru9z8spdjsgp99qchsaawzw4","bc1pqvkxuvy6cquv0x9kggy0c3skavmwh2arr22xghxae6pqwq4jk4gqw6dpu9"],"offset":0,"count":2000,"sort\_by":"inscr\_num","order":"desc"}\
headers: { "Content-Type":"application/json", "x-api-key":"...." }

#### Query Parameters

| Name                                        | Type             | Description                                                          |
| ------------------------------------------- | ---------------- | -------------------------------------------------------------------- |
| sort\_by                                    | string           | (optional) inscr\_num                                                |
| order                                       | string           | (optional) asc, desc (default: desc)                                 |
| offset<mark style="color:red;">\*</mark>    | int              | 0 <= offset                                                          |
| count<mark style="color:red;">\*</mark>     | int              | 20 <= count <= 2000                                                  |
| addresses<mark style="color:red;">\*</mark> | array of strings | bitcoin wallet addresses                                             |
| exclude\_brc20                              | string           | (optional) set to "true" (string) to exclude brc-20 inscriptions     |
| cursed\_only                                | string           | (optional) set to "true" (string) to return only cursed inscriptions |

{% tabs %}
{% tab title="200: OK Success" %}
```json
{
    "data": [
        {
            "inscription_name": "ExO Recruits #18240",
            "inscription_id": "4b0eb4278a1e65ccf9be4935bc2f9cfded27c27ce809b8227792553492053ce1i351",
            "inscription_number": 70590889,
            "parent_ids": [
                "9d71fc47daede70dde1dd4af7cdfffac18627f797d7542880ec6db2107ad62b6i0"
            ],
            "output_value": 330,
            "genesis_block_hash": "0000000000000000000042ca43ef13023e048bc83f634778dc737c5f9506e122",
            "genesis_ts": "2024-08-19T03:12:01.000Z",
            "metadata": {
                "name": "ExO Recruits #18240",
                "attributes": [
                    {
                        "value": "The Mad Scientist",
                        "trait_type": "Recruit name"
                    },
                    {
                        "value": "14",
                        "trait_type": "batch"
                    }
                ]
            },
            "owner_wallet_addr": "bc1pp5xk5dxklrfxk4yzdkel09yeqqczk5s3425zg9fj6p8qpm8axdes94yhu7",
            "mime_type": "text/plain;charset=utf-8",
            "last_sale_price": null,
            "slug": "exo_recruits",
            "collection_name": "ExO Recruits",
            "satpoint": "4b0eb4278a1e65ccf9be4935bc2f9cfded27c27ce809b8227792553492053ce1:352:0",
            "last_transfer_block_height": 841691,
            "genesis_height": 841691,
            "content_url": "https://bis-ord-content.fra1.cdn.digitaloceanspaces.com/ordinals/4b0eb4278a1e65ccf9be4935bc2f9cfded27c27ce809b8227792553492053ce1i351",
            "bis_url": "https://bestinslot.xyz/ordinals/inscription/4b0eb4278a1e65ccf9be4935bc2f9cfded27c27ce809b8227792553492053ce1i351",
            "render_url": "https://bis-ord-renders.fra1.cdn.digitaloceanspaces.com/renders/4b0eb4278a1e65ccf9be4935bc2f9cfded27c27ce809b8227792553492053ce1i351.png",
            "bitmap_number": null,
            "delegate": {
                "delegate_id": "68dddf6c9fbede5b4f6e014149946517685c4aea79250051575cb68136e8d3d9i0",
                "render_url": "https://bis-ord-renders.fra1.cdn.digitaloceanspaces.com/renders/68dddf6c9fbede5b4f6e014149946517685c4aea79250051575cb68136e8d3d9i0.png",
                "mime_type": "text/html;charset=utf-8",
                "content_url": "https://bis-ord-content.fra1.cdn.digitaloceanspaces.com/ordinals/68dddf6c9fbede5b4f6e014149946517685c4aea79250051575cb68136e8d3d9i0",
                "bis_url": "https://bestinslot.xyz/ordinals/inscription/68dddf6c9fbede5b4f6e014149946517685c4aea79250051575cb68136e8d3d9i0"
            }
        },
        ...
    ],
    "block_height": 849817
}
```
{% endtab %}
{% endtabs %}



## Get Wallet Collections

_<mark style="color:blue;">Included in: Basic, Pro, Dedicated</mark>_

<mark style="color:blue;">`GET`</mark> `https://api.bestinslot.xyz/v3/wallet/collections`

Returns ordered list of collections of a wallet.

Sample query: https://api.bestinslot.xyz/v3/wallet/collections?address=bc1pp5xk5dxklrfxk4yzdkel09yeqqczk5s3425zg9fj6p8qpm8axdes94yhu7\&sort\_by=inscription\_count\&order=desc

<mark style="color:orange;">**NOTE:**</mark> <mark style="color:orange;"></mark><mark style="color:orange;">last\_sale\_price is only available on Pro Tier.</mark>

#### Query Parameters

| Name                                       | Type   | Description              |
| ------------------------------------------ | ------ | ------------------------ |
| sort\_by<mark style="color:red;">\*</mark> | string | slug, inscription\_count |
| order<mark style="color:red;">\*</mark>    | string | asc, desc                |
| address<mark style="color:red;">\*</mark>  | string | bitcoin wallet address   |

{% tabs %}
{% tab title="200: OK Success" %}
```json
{
    "data": [
        {
            "collection_slug": "rune_pizza",
            "inscription_ids": [
                "a77c2fda458fc67028cb444b3b3fdcdf36b168d89ceb7286630d2fc76b21a714i292",
                "d8e56a07f5dc3b6ca8976502637aa50480f883ed89b46dedfcd3196a7e9e5b19i323",
                "3a94a50d3df80794c606fe1cca66d88cfcbacbe1ddafc2493d7da123ef19f4a6i771",
                "9fd85f3c8fdde5bd89525e4cfc0ad147555ef57a3f4afe01570905340e88699di1110"
            ],
            "collection_info": {
                "name": "Rune Piza",
                "slug": "rune_pizza",
                "inscription_icon_id": "https://creator-hub-prod.s3.us-east-2.amazonaws.com/ord-rune_pizza_pfp_1713024144812.jpeg",
                "icon_url": "https://creator-hub-prod.s3.us-east-2.amazonaws.com/ord-rune_pizza_pfp_1713024144812.jpeg",
                "icon_render_url": null,
                "bis_url": "https://bestinslot.xyz/ordinals/collection/rune_pizza",
                "supply": "10892",
                "min_number": 68699615,
                "median_number": 68705556,
                "max_number": 68713500,
                "listed_count": 823,
                "floor_price": 1530,
                "floor_price_ordswap": null,
                "floor_price_magiceden": 1530,
                "floor_price_ordinalswallet": 811921,
                "floor_price_gammaio": null,
                "floor_price_ordynals": null,
                "floor_price_unisat": null,
                "floor_price_ordinalsmarket": null,
                "floor_price_okx": 6000,
                "vol_3h_in_btc": 0,
                "vol_24h_in_btc": 0,
                "vol_7d_in_btc": 0,
                "vol_30d_in_btc": 0,
                "sale_cnt_7d": 0,
                "vol_total_in_btc": 23.96608198,
                "sale_cnt_total": 4921,
                "marketcap": 16664760
            }
        },
        ...
    ],
    "block_height": 889397
}
```
{% endtab %}

{% tab title="429: Too Many Requests Rate limit exceeded" %}

{% endtab %}
{% endtabs %}



## Get Wallet Verified Sats

_<mark style="color:blue;">Included in: Basic, Pro, Dedicated</mark>_

<mark style="color:blue;">`GET`</mark> `https://api.bestinslot.xyz/v3/wallet/sats_names`

Returns list of verified sats names of a wallet.

Sample query: https://api.bestinslot.xyz/v3/wallet/sats\_names?address=bc1p4wj6n9c80zvrjwq3lke2n8esuv8rzw6ch0jlqfrlpanlyn3ftx2s6dgwec

#### Query Parameters

| Name                                      | Type   | Description            |
| ----------------------------------------- | ------ | ---------------------- |
| address<mark style="color:red;">\*</mark> | string | bitcoin wallet address |

{% tabs %}
{% tab title="200: OK Success" %}
```json
{
    "data": [
        {
            "name": "aui.sats",
            "inscription_id": "8279ab4057df0fcee4eb7c0047acc2f3de3fbd84bd149b0d8f5e4af95988fe13i0",
            "inscription_number": 264143
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



## Get Wallet Listings

_<mark style="color:blue;">Included in: Pro, Dedicated</mark>_

<mark style="color:blue;">`GET`</mark> `https://api.bestinslot.xyz/v3/wallet/listings`

Returns ordered list of listings of a bitcoin wallet.

Sample query: https://api.bestinslot.xyz/v3/wallet/listings?address=bc1par0t76nmjf55wp0rpzu58p97mzz6tf3cd67js077a2qx5ez8knlqfnccjq\&sort\_by=min\_price\&order=asc\&offset=0\&count=100

#### Query Parameters

| Name                                       | Type   | Description                                                                                                                                           |
| ------------------------------------------ | ------ | ----------------------------------------------------------------------------------------------------------------------------------------------------- |
| sort\_by<mark style="color:red;">\*</mark> | string | min\_price, ordswap\_price, magiceden\_price, ordinalswallet\_price, gammaio\_price, odynals\_price, unisat\_price, ordinalsmarket\_price, okx\_price |
| order<mark style="color:red;">\*</mark>    | string | asc, desc                                                                                                                                             |
| offset<mark style="color:red;">\*</mark>   | int    | 0 <= offset <= 5k                                                                                                                                     |
| count<mark style="color:red;">\*</mark>    | int    | 20 <= count <= 100                                                                                                                                    |
| address<mark style="color:red;">\*</mark>  | string | bitcoin wallet address                                                                                                                                |

{% tabs %}
{% tab title="200: OK Success" %}
```json
{
    "data": [
        {
            "inscription_id": "2506d91d5f9827da5aa604dcf38918317ad58e884be269e823706ebd330758cfi0",
            "min_price": 999993,
            "ordswap_price": null,
            "magiceden_price": null,
            "ordinalswallet_price": 999993,
            "gammaio_price": null,
            "nostr_price": null,
            "odynals_price": null,
            "unisat_price": null,
            "ordinalsmarket_price": null,
            "okx_price": null,
            "owner_wallet_addr": "bc1par0t76nmjf55wp0rpzu58p97mzz6tf3cd67js077a2qx5ez8knlqfnccjq"
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



## Get Wallet Activity (Inscriptions Only)

_<mark style="color:blue;">Included in: Pro, Dedicated</mark>_

<mark style="color:blue;">`GET`</mark> `https://api.bestinslot.xyz/v3/wallet/activity`

Returns ordered list of inscribes, sales and transfers of a bitcoin wallet.

Sample query: https://api.bestinslot.xyz/v3/wallet/activity?address=bc1par0t76nmjf55wp0rpzu58p97mzz6tf3cd67js077a2qx5ez8knlqfnccjq\&activity\_filter=7\&sort\_by=ts\&order=desc\&offset=0\&count=100

#### Query Parameters

| Name                                               | Type   | Description                                                                                                                  |
| -------------------------------------------------- | ------ | ---------------------------------------------------------------------------------------------------------------------------- |
| sort\_by<mark style="color:red;">\*</mark>         | string | ts                                                                                                                           |
| order<mark style="color:red;">\*</mark>            | string | asc, desc                                                                                                                    |
| offset<mark style="color:red;">\*</mark>           | int    | 0 <= offset <= 5k                                                                                                            |
| count<mark style="color:red;">\*</mark>            | int    | 20 <= count <= 100                                                                                                           |
| address<mark style="color:red;">\*</mark>          | string | bitcoin wallet address                                                                                                       |
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



## Get Wallet Global Activity (Inscriptions, BRC20 and Runes)

_<mark style="color:blue;">Included in: Dedicated</mark>_

<mark style="color:blue;">`GET`</mark> `https://api.bestinslot.xyz/v3/wallet/global_activity`

Returns ordered list of inscription, brc20 and runes activities of bitcoin wallet.\
This endpoint is the combined view of: `/v3/wallet/activity`, `/v3/brc20/wallet_activity` and `/v3/runes/wallet_activity`

Response will have mixed structures since different protocols require different fields.

```
InscriptionStructure: {
  event_category: 'inscription',
  event_type: 'inscribe' | 'transfer' | 'buy' | 'sell',
  inscription_id,
  tx_id,
  new_satpoint,
  from_wallet, to_wallet,
  block_height, ts,
  amount: 1,
  sale_price,
  unit_price: same as sale_price for this type,
  marketplace_type: marketplace_type on Constants tab,
  inner_id: for debugging purposes
}
BRC20Structure: {
  event_category: 'brc20',
  event_type: 'deploy-inscribe' | 'mint-inscribe' | 'transfer-inscribe' | 'transfer-transfer',
  inscription_id,
  tx_id,
  new_satpoint,
  from_wallet, to_wallet,
  block_height, ts,
  amount,
  sale_price,
  unit_price,
  marketplace_type: marketplace_type on Constants tab,
  ticker,
  inner_id: for debugging purposes
}
RunesStructure: {
  event_category: 'runes',
  event_type: 'input' | 'new-allocation' | 'mint' | 'output' | 'burn',
  outpoint,
  tx_id,
  wallet_addr,
  block_height, ts,
  amount,
  sale_price,
  sold_to_wallet_addr,
  marketplace_type: marketplace_type on Constants tab,
  rune_id, rune_name, spaced_rune_name, decimals,
  inner_id: for debugging purposes
}
```

For runes events response structure, please check `/v3/runes/wallet_activity` endpoint details.

Since a single runes transaction can have a lot of runes events, if the last runes event does not fit into count, the endpoint will return all events in the tx anyway. So, the response may have more elements than count.

Sample query: https://api.bestinslot.xyz/v3/wallet/global\_activity?address=bc1pg7j3rwqnjfsrj66gcgtfx99c6l3vnrs9v7arx3kpjmh9ukmv47wq0jdgg0\&sort\_by=ts\&order=desc\&count=500\&cursor=384298391\_\_14396391

#### Query Parameters

| Name                                       | Type     | Description                                                |
| ------------------------------------------ | -------- | ---------------------------------------------------------- |
| sort\_by<mark style="color:red;">\*</mark> | `string` | ts                                                         |
| order<mark style="color:red;">\*</mark>    | `string` | asc, desc                                                  |
| count<mark style="color:red;">\*</mark>    | `int`    | 20 <= count <= 500                                         |
| address<mark style="color:red;">\*</mark>  | `string` | bitcoin wallet address                                     |
| runes\_filter\_only\_wallet                | `string` | (optional) "true" or "false"                               |
| cursor                                     | `string` | to continue fetching data, use the cursor on last response |

{% tabs %}
{% tab title="200: OK Success" %}
```json
{
    "data": {
        "cursor": "1117389_32620821_11504547",
        "result": [
            {
                "event_category": "inscription",
                "event_type": "transfer",
                "inscription_id": "382c9ce1b42bec9fff3c20cd450ea22f0f7c538824dcebb16e09028b486bf5a4i530",
                "tx_id": "f9b6dbe3012fb83eebd4f475d3802650f54192226d40d8dab8ef8645586cda82",
                "new_satpoint": "f9b6dbe3012fb83eebd4f475d3802650f54192226d40d8dab8ef8645586cda82:0:0",
                "from_wallet": "bc1pjlqse9nd2q45lauevagerrka3vnmq5ksnph7muztuhkl0d26kgusj9n42c",
                "to_wallet": "bc1pg7j3rwqnjfsrj66gcgtfx99c6l3vnrs9v7arx3kpjmh9ukmv47wq0jdgg0",
                "block_height": 842074,
                "ts": "2024-05-04T15:29:49.000Z",
                "amount": 1,
                "sale_price": -1,
                "unit_price": -1,
                "marketplace_type": "",
                "inner_id": 379499237
            },
            {
                "event_category": "runes",
                "event_type": "output",
                "outpoint": "592ce71f4c962a18565c1d7db5336f956d5af48d2b46b21d19c001b79272d565:0",
                "tx_id": "592ce71f4c962a18565c1d7db5336f956d5af48d2b46b21d19c001b79272d565",
                "wallet_addr": "bc1pg7j3rwqnjfsrj66gcgtfx99c6l3vnrs9v7arx3kpjmh9ukmv47wq0jdgg0",
                "block_height": 841974,
                "ts": "2024-05-03T22:37:46.000Z",
                "amount": "2280",
                "sale_price": null,
                "sold_to_wallet_addr": null,
                "marketplace_type": "unindexed",
                "rune_id": "841599:714",
                "rune_name": "BUTTERNUTTHEHELLCAT",
                "spaced_rune_name": "BUTTERNUT•THE•HELL•CAT",
                "decimals": 0,
                "inner_id": 13122494
            },
            {
                "event_category": "runes",
                "event_type": "input",
                "outpoint": "6c7ebb818b94bc3c68e6681fde4bfc4a726a9bf002ca7400fb703cb9f0fe3539:2",
                "tx_id": "592ce71f4c962a18565c1d7db5336f956d5af48d2b46b21d19c001b79272d565",
                "wallet_addr": "bc1p9gvz9w89j60y2xy9pycmfls5xl5y0kklgdcfxf7tqyhfdre9wdeq8etlru",
                "block_height": 841974,
                "ts": "2024-05-03T22:37:46.000Z",
                "amount": "1140",
                "sale_price": 502146,
                "sold_to_wallet_addr": "bc1pg7j3rwqnjfsrj66gcgtfx99c6l3vnrs9v7arx3kpjmh9ukmv47wq0jdgg0",
                "marketplace_type": "magiceden",
                "rune_id": "841599:714",
                "rune_name": "BUTTERNUTTHEHELLCAT",
                "spaced_rune_name": "BUTTERNUT•THE•HELL•CAT",
                "decimals": 0,
                "inner_id": 13122493
            },
            {
                "event_category": "runes",
                "event_type": "input",
                "outpoint": "6c7ebb818b94bc3c68e6681fde4bfc4a726a9bf002ca7400fb703cb9f0fe3539:1",
                "tx_id": "592ce71f4c962a18565c1d7db5336f956d5af48d2b46b21d19c001b79272d565",
                "wallet_addr": "bc1p9gvz9w89j60y2xy9pycmfls5xl5y0kklgdcfxf7tqyhfdre9wdeq8etlru",
                "block_height": 841974,
                "ts": "2024-05-03T22:37:46.000Z",
                "amount": "1140",
                "sale_price": 502146,
                "sold_to_wallet_addr": "bc1pg7j3rwqnjfsrj66gcgtfx99c6l3vnrs9v7arx3kpjmh9ukmv47wq0jdgg0",
                "marketplace_type": "magiceden",
                "rune_id": "841599:714",
                "rune_name": "BUTTERNUTTHEHELLCAT",
                "spaced_rune_name": "BUTTERNUT•THE•HELL•CAT",
                "decimals": 0,
                "inner_id": 13122492
            },
            ...
        ]
    },
    "block_height": 847622
}
```
{% endtab %}
{% endtabs %}



## Get Wallet Metadata

_<mark style="color:blue;">Included in: Basic, Pro, Dedicated</mark>_

<mark style="color:blue;">`GET`</mark> `https://api.bestinslot.xyz/v3/wallet/metadata`

Returns inscription\_count, nonbrc20\_inscription\_count and last\_transfer\_block\_height for a given wallet address.

Sample query: https://api.bestinslot.xyz/v3/wallet/metadata?address=bc1p4wj6n9c80zvrjwq3lke2n8esuv8rzw6ch0jlqfrlpanlyn3ftx2s6dgwec

#### Query Parameters

| Name                                      | Type   | Description            |
| ----------------------------------------- | ------ | ---------------------- |
| address<mark style="color:red;">\*</mark> | string | bitcoin wallet address |

{% tabs %}
{% tab title="200: OK Success" %}
```json
{
    "data": {
        "inscription_count": 5,
        "nonbrc20_inscription_count": 5,
        "last_transfer_block_height": 779081
    },
    "block_height": 801647
}
```
{% endtab %}

{% tab title="429: Too Many Requests Rate limit exceeded" %}

{% endtab %}
{% endtabs %}
