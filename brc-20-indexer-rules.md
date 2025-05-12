---
description: Detailed rules of BRC-20 Indexing
---

# BRC-20 Indexer Rules

In order to not conflict with the current indexers, we followed [Unisat's open-source indexer](https://github.com/unisat-wallet/libbrc20-indexer) whenever necessary, also we followed all of the rules at the [official BRC-20 gitbook](https://domo-2.gitbook.io/brc-20-experiment/). In addition to these rules, we extensively checked BRC-20 tokens / token movements and cross checked it with other indexers to not have any indexing conflicts.

Here are the detailed indexing rules that we follow:

* **Inscription must have a MIME Type of "text/plain" or "application/json".** To check this, split the mime type from ";" and check the first part without strip/trim etc.
* Inscription must be a valid JSON (**not** JSON5)
* JSON must have "p", "op", "tick" fields where "p"="brc-20", "op" in \["deploy", "mint", "transfer"]
  * If op is deploy, JSON must have a "max" field. "lim" and "dec" fields are optional. If "dec" is not set, it will be counted as 18. If "lim" is not set it will be equal to "max".
  * If op is mint or transfer, JSON must have an "amt" field.
* **ALL NECESSARY JSON FIELDS MUST BE STRINGS.** Numbers at max, lim, amt, dec etc. are not accepted. **Extra fields which haven't been discussed here can be of any type.**
* **Numeric fields are not stripped/trimmed.** "dec" field must have only digits, other numeric fields may have a single dot(".") for decimal representation (+,- etc. are not accepted). Decimal fields **cannot start or end with dot** (e.g. ".99" and "99." are invalid).
* **Empty string for numeric field is invalid.**
* **0 for numeric fields is invalid except for "dec" field.**
* If any decimal representation have **more decimal digits** than "dec" of ticker, the inscription will be counted as invalid **(even if the extra digits are 0)**
* Max value of "dec" is 18.
* Max value of any numeric field is uint64\_max.
* "tick" must be 4bytes wide (UTF-8 is accepted). "tick" is **case insensitive**, we use lowercase letters to track tickers (convert tick to lowercase before processing).
* If a deploy, mint or transfer is **sent as fee** to miner while inscribing, it **must be ignored**
* If a transfer is **sent as fee** in its first transfer, its amount **must be returned to sender**
* If a mint has been deployed with more amt than lim, it will be ignored.
* If a transfer has been deployed with more amt than **available balance** of that wallet, it will be ignored.
* **All balances are followed using scriptPubKey** since some wallets may not have an address attached on bitcoin.

How the protocol works:

* First a deploy inscription is inscribed. This will set the rules for this brc-20 ticker. If the same ticker (case insensitive) has already been deployed, **the second deployment will be invalid**.
* Then anyone can inscribe mint inscriptions with the limits set in deploy inscription until the minted balance reaches to "max" set in deploy inscription.
* **The last mint inscription will mint the remaining tokens**. For example, if the ticker only has 100 tokens left but a mint inscription wants to mint 500, it will mint the remaining 100 tokens.
* When a wallet mints a brc-20 token (inscribes a mint inscription to its address), its **overall balance** and **available balance** will increase.
* Wallets can inscribe transfer inscriptions with amount **up to their available balance**.
* If a user inscribe a transfer inscription but does not transfer it, its overall balance will stay the same but its available balance will decrease.
* When this transfer inscription is transferred **(not sent as fee to miner)** the original wallet's overall balance will decrease but its available balance will stay the same. The receiver's overall balance and available balance will increase.
* If you transfer the transfer inscription to your own wallet, your available balance will increase and the transfer inscription will become used.
* **A transfer inscription will become invalid/used after its first transfer.**
* **Buying, transferring mint and deploy inscriptions will not change anyone's balance.**

Some possible pitfalls:

* JS integer is actually double floating point number and it can only hold 53-bit integers with full-precision. **If you want to make an indexer with JS, use BigInt.**
* Sent as fee rule is very important and needs to be handled carefully.
* **Do not use string length for ticker length comparison.** Some UTF-8 characters like most of the emojis use 4bytes but their string length is 1 on most programming languages.
* Numeric fields does not accept numeric values. Use strings in JSON.
* Do not trim/strip any field.
* Do not use int/float conversion directly on numeric fields. For example some languages may accept "123asd" as valid integer with 123 value but this inscription is invalid.
* Check decimal length of amt, max, lim from string value. Extra 0's at the end of the decimal part may invalidate the token if there are more decimal digits than "dec" of ticker.
* **Beware of the reorgs.** Since the order of transactions is very important in this protocol, a reorg will probably change the balances.
