# Changelog

### 25/Mar/2025

* Removed all offset and count limits from dedicated servers.
* Endpoint <kbd>/v3/collection/holders</kbd> now returns the original wallet address if the inscription is locked using `Ordinal Lockers`.
* Added optional `runes_filter_only_wallet`  parameter to `/v3/runes/wallet_activity` and `/v3/wallet/global_activity`&#x20;
* Added dedicated only mempool endpoints:
  * `/v3/mempool/all_runic_utxos`
  * `/v3/mempool/all_ordinal_utxos`
  * `/v3/mempool/all_cardinal_utxos`
  * `/v3/mempool/all_runes_events`
* Added optional `send_urls` parameter to `/v3/runes/all_id_name_pairs`&#x20;
* Added `/v3/runes/historical_total_supply`  endpoint
* Added `vol_3h_in_btc` and `vol_30d_in_btc` to `/v3/collection/collections` response
* Added optional `collection_slug` parameter to `/v3/wallet/inscriptions`&#x20;
* Added `/v3/wallet/collections` endpoint
* Added `/v3/inscription/render_refresh` endpoint
* Increased count limit on `/v3/brc20/tickers` and `/v3/runes/tickers` to `300`.
* Added optional `granularity` parameter to `/v3/runes/historical_prices`

### 01/Oct/2024

* Added Mempool & UTXO related APIs.

{% content-ref url="mempool.md" %}
[mempool.md](mempool.md)
{% endcontent-ref %}

### 27/Sep/2024

* Added `output_value`, `genesis_ts`, `genesis_block_hash` to `wallet/inscriptions` and `wallet/inscriptions_batch`
* Added `genesis_block_hash` to `inscription/batch_info`
* Added more granular sale\_count to `runes/sales_info.` Also, total\_sale\_info field on `runes/tickers` and runes/ticker\_info also includes this more granular sale\_count information.
* Added `icon_content_url` and `icon_render_url` to `runes/wallet_activity`
* Converted `balances` from `int array` to `string array` for better precision on:
  * `runes/wallet_valid_outputs`
  * `runes/wallet_valid_outputs_single_rune`
  * `runes/output_info`
  * `runes/batch_output_info`
  * `runes/valid_outputs`
* Added new enterprise only endpoint: `runes/all_id_name_pairs`
* Added new dedicated only endpoint: `runes/historical_prices`

### 02/Jul/2024

* Added Unisat floor prices to collection and bitmap endpoints (`collection/market_info`, `collection/collections`, `bitmap/market_info`)
* Added OKX listings to brc20 endpoints (`brc20/tickers`, `brc20/market_info`, `brc20/validtxnotes`, `brc20/validtxnotes_wallet`, `brc20/listings`)
* Added batch version of `wallet/inscriptions` at `wallet/inscriptions_batch` for PRO users.

### 17/Jun/2024

* Enabled testnet4 API at `https://testnet.api.bestinslot.xyz`
* Added tBTC faucet at `/v3/wallet/testnet_faucet`

### 12/Jun/2024

* Added runes icon information to `runes/tickers` and `runes/ticker_info`. New fields are: `icon_inscr_id, icon_delegate_id, icon_content_url, icon_render_url`
* Added global activity endpoint (combined view of ordinals, brc20 and runes) to dedicated servers: `/v3/wallet/global_activity`

### 30/May/2024

* Added optional `rune_id`, `rune_name`, `rune_number` filter to `runes/wallet_activity` endpoint.

### 23/May/2024

* Added `brc20/wallet_activity` endpoint
* Added `rune_number` as optional input on all endpoints that accepts `rune_id` as input
* Improved performance on runes balances related endpoints
* Added `total_volume` sorting to `runes/tickers`
* Added `avg_unit_price_in_sats`, `min_listed_unit_price_in_sats`, `listed_supply`, `listed_supply_ratio`, `marketcap` and `total_sale_info` fields to `runes/ticker_info` for PRO API Keys
* Added `runes/ticker_cnt` endpoint
* Increased limit for `runes/holders` to 5000 for PRO API Keys

### 30/Apr/2024

* Updated price calculation algorithm used in runes to use the median unit price.
* Added listing information to runes endpoints:
  * Added `min_listed_unit_price_in_sats` and `min_listed_unit_price_unisat` to `runes/wallet_balances`
  * Added `min_listed_unit_price_in_sats`, `min_listed_unit_price_unisat`, `listed_supply` and `listed_supply_ratio` to `runes/tickers`
  * Added `min_price`, `min_unit_price`, `unisat_price`, `unisat_unit_price` to `runes/valid_outputs`
  * Added `min_price` and `unisat_price` to `runes/wallet_valid_outputs`
  * Added new endpoints: `runes/market_info`, `runes/listings`, `runes/wallet_valid_outputs_single_rune`

### 25/Apr/2024

* Added signet support via endpoint: `https://signet_api.bestinslot.xyz`

### 24/Apr/2024

* Added Magic Eden support to Runes sales indexing. (Since sales are indexed directly from the chain, we actually support almost all current and future marketplaces already, this support is only for distinguishing which sale happened on which marketplace)\
  Currently supporting:
  * Unisat
  * OKX
  * Ordinals Wallet
  * Magic Eden

### 23/Apr/2024

* Added decimals to all related runes endpoints:
  * `runes/wallet_balances`, `runes/wallet_valid_outputs`, `runes/holders`, `runes/output_info`, `runes/batch_output_info`, `runes/valid_outputs`, `runes/activity`, `runes/wallet_activity`, `runes/events_on_tx`, `runes/activity_on_block`

### 22/Apr/2024

* Added on-chain sale information to runes endpoints. These changes are only available on PRO API-Keys
  * `runes/tickers` added `avg_unit_price_in_sats`, `marketcap`, 3h-6h-9h-12h-1d-3d-7d-30d-total `volumes`, `sale count` and `sale amount` (total sold amount). Also added `avg_unit_price_in_sats` and `marketcap` orderings.
  * `runes/wallet_balances` added `avg_unit_price_in_sats`
  * Added `runes/sales_info` endpoint.
  * Added sale\_info field to `runes/activity`, `runes/wallet_activity`, `runes/events_on_tx` and `runes/activity_on_block`.  If the event is a sale event, this will not be null and it'll be an object including `sale_price, sold_to_pkscript, sold_to_wallet_addr, marketplace` properties.
* Added `decimals` to `runes/wallet_balances`
* `avg_unit_price_in_sats` => Calculated by taking the average unit price of sales in last 6 hrs. If there are not enough sale in last 6 hrs, it'll look at latest several sales, if there is not enough sale on the ticker, it'll return null. Note that this is scaled by decimals to make ordering more meaningful.

### 15/Apr/2024

* Updated runes backend to ord 0.18.1
* Added new **auto\_upgrade**(turbo) field to rune information endpoints. `runes/tickers`, `runes/ticker_info`
* Enabled runes API on `mainnet`.

### 11/Apr/2024

* Added `/v3/runes/testnet_faucet` where users with API-Key can request testnet rune 10 times per 24 hours.
  * The returned rune has decimals: 8
  * The mint amount is 1.0 (1\_0000\_0000)
  * If the faucet drains, it'll stop working so any tBTC contribution to `tb1pxph9qxtvszufzt4qfk4ftxxkg3jrwdypdjkqxj9zwtcl0kwu8qkqu7df8n` is appreciated.

### 05/Apr/2024

* Added Testnet Runes support

### 29/Mar/2024

* Updated inscription suite to ord v0.16.0
* Added delegate and parent ids support.
* Added rendered urls for recursive inscriptions. Rendering is done asynchronously so some new recursive inscriptions may not have rendered images yet.
* On collection information endpoints: `icon_render_url` field is added for recursive inscription icons of some collections. Also, if collection\_icon is an inscription id and that inscription has an inscribed delegate, `icon_render_url` and `icon_url` will use delegate inscription information. `collection/info, collection/collections`
* On inscription information endpoints: `parent_ids`, `render_url` and `delegate` fields are added. `delegate` field has `delegate_id`, `render_url`, `mime_type`, `content_url` and `bis_url` subfields. If the inscription doesn't have `delegate_id` set, then `delegate` field will be `null`. If the inscription does have `delegate_id` set but this id hasn't been inscribed yet, then only `delegate_id` subfield will have value, others will be `null`. collection/inscriptions, wallet/inscriptions, inscription/single\_info\_id, inscription/batch\_info, inscription/new\_inscriptions\_in\_block

### 29/Mar/2024

* Updated whole metaprotocol suite to OPI v0.4.0
* Added original\_ticker, is\_self\_mint and burned\_supply to ticker info endpoints: `brc20/tickers, brc20/ticker_info`&#x20;
* Added original\_ticker, parent\_id and is\_self\_mint to event endpoints: `brc20/single_info, brc20/batch_info, brc20/activity_on_block`

### 12/Mar/2024

* Added `bitmap_number` to `inscription/single_info_id, inscription/batch_info, inscription/new_inscriptions_in_block and wallet/inscriptions`.

### 08/Jan/2024

* Added `byte_size` to `inscription/single_info_id, inscription/batch_info, inscription/new_inscriptions_in_block`.
* Added `listed_count, floor_price, floor_price_ordswap, floor_price_magiceden, floor_price_ordinalswallet, floor_price_gammaio, floor_price_ordynals, floor_price_ordinalsmarket, floor_price_okx, vol_24h_in_btc, vol_7d_in_btc, sale_cnt_7d, vol_total_in_btc, sale_cnt_total, marketcap` to **pro tier** `collection/collections`.
* Added `brc20/event_from_txid` endpoint.
* Added optional `wallet` filter to `brc20/activity`.

### 04/Jan/2024

* Updated metaprotocol backend to OPI v0.2.0 which uses ord 0.14.0 with vindicated charm added.

### 20/Dec/2023

* Added OrdinalNovus to Sale Marketplace Identifier.
* Increased page size of `wallet/inscriptions`, `brc20/validtxnotes` and `brc20/validtxnotes_wallet` to 2000.
* Moved `brc20/validtxnotes` and `brc20/validtxnotes_wallet` to Basic API category.
* Added optional `cursed_only` filter to `wallet/inscriptions`.

### 19/Dec/2023

* Updated to ord v0.12.3
* BRC20 and Bitmap backend now uses [OPI](https://github.com/bestinslot-xyz/OPI).
* Added `brc20/batch_info` endpoint.
* Added new fields to response of `brc20/tickers`.

### 09/Nov/2023

* Added `inscription/activity_on_block` enterprise endpoint.

### 08/Nov/2023

* Improved performance of brc20 balance\_on\_block endpoints.
* Increased query limit of `batch_balance_on_block` to 100.

### 07/Nov/2023

* Upgraded API backend to ord 0.9.0
* Opened testnet API

### 01/Nov/2023

* Added sub1k and sub10k meta-collections.
* Added `brc20/batch_balance_on_block` enterprise endpoint.
* Added `owner_wallet_addr` to all listing endpoints.

### 27/Oct/2023

* Added `/v3/brc20/all_validtxnotes` and `/v3/brc20/all_balances` enterprise endpoints.
* Added `bitmap` endpoints.

### 01/Sep/2023

* Added new Magic Eden Batch Sale type to our sale-indexer and marketplace-indexer. All missing sales have been indexed.
* Added `inscription/new_inscriptions_in_block` Enterprise endpoint.
* Added `ticker` to the response of `brc20/validtxnotes_wallet`.
* Added `satpoint` to the responses of `brc20/validtxnotes` and `brc20/validtxnotes_wallet`
* Added optional `ticker` filter to `brc20/wallet_balances`
* Added `old_satpoint` and `new_satpoint` to the response of `brc20/activity_on_block`
* Added `sale_amount` (how many tokens have been sold) to the response of `brc20/sales_info`
* Added optional `last_new_satpoint` parameter to `brc20/activity` too. It works the same as `collection/activity`
* Fixed `collection/holders` response for an empty collection. Now the endpoint returns an empty array.

### 23/Aug/2023

* added brc20/activity\_on\_block and brc20/balance\_on\_block Enterprise endpoints.

### 22/Aug/2023

* added brc20/validtxnotes\_wallet to get valid brc-20 tx notes of a given wallet address
* added inscription/global\_info which returns total count of inscriptions, count of different mime types, and some global volume information
* added inscription/batch\_info which returns information about multiple inscriptions (up to 100) using their number or id or location (utxo)
* added nonbrc20\_inscription\_count to wallet/metadata

### 11/Aug/2023

* added okx listings to API
  * collection/market\_info
  * collection/listings
  * wallet/listings
  * inscription/single\_info\_id
* added brc20/activity\_on\_block endpoint
* added brc20/balance\_on\_block endpoint
* optimised indexer and queries

### 04/Aug/2023

* added exclude\_brc20 to wallet/inscriptions
* added wallet/metadata endpoint
* added sats/activity endpoint
* increased count limit on wallet/inscriptions to 500
* added optional paging to collection/holders
* return only listed items on collection/listings & wallet/listings & brc20/listings
* made api-key mandatory, apply for a free/trial key to test our API
* enabled auto transition to free-tier when a key got expired
* fixed a problem about unisat/okx sale marketplace identification

### 24/Jul/2023

* collection/sales\_info and brc20/sales\_info now supports setting a marketplace to get statistics for only selected marketplace
* collection/activity wallet/activity and inscription/activity now returns marketplace\_type on sale events
* collection/inscriptions and wallet/inscriptions now returns genesis\_height too
* brc20/tickers now uses an optional minting\_status parameter to filter tickers based on their minting status
