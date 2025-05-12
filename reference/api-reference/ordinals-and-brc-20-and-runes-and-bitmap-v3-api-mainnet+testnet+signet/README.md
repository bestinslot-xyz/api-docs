# Ordinals & BRC-20 & Runes & Bitmap V3 API (mainnet+testnet+signet)

### Rate Limiting

There are 4 API-Key categories: `Basic`, `Pro`, `Enterprise` and `Dedicated`. Some endpoints are only available in some plans. Rate limit categories can be found on [bestinslot.xyz/api](https://bestinslot.xyz/api/). Free plan and trial key are rate limited with daily limits, all other plans uses monthly limits. All plans require an API-Key so even if you want to use our free plan or trial plan, you should contact us via [this form](https://coda.io/form/Best-in-Slot-API-Request-Form_dbtfCuBhaEy).

Endpoints' API-Key-Tier availabilities are written for each endpoint in documentation.

Expired API-Keys automatically turn into Free-Tier API Key.

### General Usage Information

* API Key should be sent in `x-api-key` header.
* Offset is limited to 5000 for most endpoints. Some endpoints may have increased offset limit or may not have an offset limit (such as `brc20/holders`), please see the parameter list to check limits.
* Maximum count value is 100 for most endpoints. Some endpoints may have increased count limit (such as `brc20/holders`), please see the parameter list to check limits.
* Offset and count must be a multiple of 20.

An example curl request to `brc20/ticker_info` with an API Key:

```powershell
curl --location 'https://api.bestinslot.xyz/v3/brc20/ticker_info?ticker=ordi' \
--header 'x-api-key: xxxx'
```

### **Response Scheme**

```
{
    "data": ... ,
    "block_height": 805712
}
```

Here, block\_height in the response indicates the **latest indexed** block height.

### Testnet & Signet API

To use our full API running on Bitcoin Testnet4 or Signet, just use `https://testnet.api.bestinslot.xyz` or `https://signet_api.bestinslot.xyz` respectively on your requests. Same API-Keys can be used on testnet4 and signet.

## Categories

{% content-ref url="mempool.md" %}
[mempool.md](mempool.md)
{% endcontent-ref %}

{% content-ref url="collections.md" %}
[collections.md](collections.md)
{% endcontent-ref %}

{% content-ref url="wallets.md" %}
[wallets.md](wallets.md)
{% endcontent-ref %}

{% content-ref url="inscriptions.md" %}
[inscriptions.md](inscriptions.md)
{% endcontent-ref %}

{% content-ref url="sats-names.md" %}
[sats-names.md](sats-names.md)
{% endcontent-ref %}

{% content-ref url="brc-20.md" %}
[brc-20.md](brc-20.md)
{% endcontent-ref %}

{% content-ref url="runes.md" %}
[runes.md](runes.md)
{% endcontent-ref %}

{% content-ref url="bitmap.md" %}
[bitmap.md](bitmap.md)
{% endcontent-ref %}

{% content-ref url="bip-322.md" %}
[bip-322.md](bip-322.md)
{% endcontent-ref %}



{% content-ref url="changelog.md" %}
[changelog.md](changelog.md)
{% endcontent-ref %}
