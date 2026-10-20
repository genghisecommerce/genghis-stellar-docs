# 6. Product delivery

Genghis has shipped a live marketplace with its own checkout, a public read-only server for AI agents, and a Stellar testnet proof of concept. The Stellar payment path is not in production. This page keeps the three apart.

## LIVE on genghis.pro today

| Item | What it is | Since | Link |
|---|---|---|---|
| Marketplace | 4,500+ products in stock, delivered digitally (page 4) | October 2025 on the rebuilt platform | https://www.genghis.pro |
| In-house checkout | Replaced the third-party payment redirect. The customer pays on genghis.pro in any of 221 cryptocurrencies (265 coin and network options, read 23 September 2026) through a licensed processor and the code appears on screen and by email. | 25 August 2026 | https://www.genghis.pro |
| Automatic fulfilment | Paid orders are bought from the supplier and the code is returned by the system. eSIMs are delivered in about 8 seconds. Exceptions are handled by hand. | Throughout 2026 | |
| Purchase limits | Rolling limits per card, per day and per month, version 2 | 25 September 2026 | |
| Loyalty points and refunds | Points on purchases. Refunds by Points or by crypto payout. | 2026 | |
| Three more languages | German, Spanish, Turkish | 8, 11 and 13 October 2026 | |
| Help Center | 145 English articles | 2026 | https://help.genghis.pro |
| Developer page for agents | Describes the catalogue server and `llms.txt` | 25 September 2026 | https://www.genghis.pro/developers |

## LIVE as public code: the read-only MCP server

[genghis-mcp-readonly](https://github.com/genghisecommerce/genghis-mcp-readonly) is a Model Context Protocol server over the live catalogue.

- Six tools: search products, get a product, compare a brand across country markets, list countries, list categories, and read how to pay.
- Read only. It holds no credentials. A guard refuses any write request before it leaves the process, so it adds no attack surface.
- Test suites pass against production on two versions of the protocol SDK.
- An agent connected to it can find and price a product. It cannot pay. The payment gap is what the grant closes.

Published 25 September 2026. Submissions to public MCP directories are open and not yet listed as of 20 October 2026.

## TESTNET: the Stellar proof of concept

Live page: https://genghisecommerce.github.io/genghis-stellar-poc/ Code: [genghis-stellar-poc](https://github.com/genghisecommerce/genghis-stellar-poc)

A Genghis-branded purchase flow on Stellar testnet. The reviewer journey:

1. Open a product page: India eSIM, Singapore eSIM or an Amazon US gift card. Prices are the live Genghis USD prices, read on 20 October 2026.
2. Choose a plan or value.
3. Choose USDC (shown first, the default) or XLM. The XLM quote uses the live XLM to USD rate and expires after two minutes.
4. Connect a wallet through Stellar Wallets Kit (Freighter, xBull, Albedo or Hana) set to testnet.
5. Approve the payment in the wallet. It settles in about five seconds.
6. See the confirmation: payment matched to the order by memo, asset and amount, the transaction link, and the delivered code.

Asset decision (20 October 2026): **USDC is primary, received directly on a Genghis-owned Stellar account. XLM is secondary, through the current payment processor.**

| Working on testnet | Simulated in the demo | Built by the grant |
|---|---|---|
| Live Genghis products, values and USD prices | The order is created in the browser, not in the Genghis order system | This checkout inside genghis.pro, on mainnet |
| Wallet connection through Stellar Wallets Kit | The delivered code is a placeholder. No supplier is called. | USDC received on a Genghis Stellar account, with a payment listener in the order system |
| USDC by default, XLM as the alternative | The receiving account is a testnet account made for the demo | XLM through the current processor |
| A payment signed in the wallet and settled on testnet | A wallet with no testnet USDC pays in XLM, converted on the Stellar DEX in the same transaction, so Genghis still receives the exact USDC amount | The real code delivered the moment the payment settles |
| A listener that reads the Genghis account on Horizon and matches memo, asset and amount before anything is delivered | | Agent purchases over x402 on Stellar, paid in USDC |

### Testnet transactions

Both were checked on Stellar testnet on 20 October 2026: successful.

| Date | What | Transaction |
|---|---|---|
| 25 September 2026 | Wallet payment from the first proof of concept: 5 test XLM, memo `GX307203126`, page returned the placeholder code. Verified by the founder with Freighter. | [6e6c4398d7a0e650a0195b39310e23cacfe02aea83ad0a0aeaf0a587285222b4](https://stellar.expert/explorer/testnet/tx/6e6c4398d7a0e650a0195b39310e23cacfe02aea83ad0a0aeaf0a587285222b4) |
| 25 September 2026 | Agent prototype run: an agent found an Amazon USD 70 gift card ($71.73) through the MCP server, received an HTTP 402 payment request with amount, address and memo, paid 325.79 test XLM with memo `GX681871822` and received the code in the response. | [9705c4f2789a499efb101d12aa37e9f76d09b69250df61e6629ee6318e710a97](https://stellar.expert/explorer/testnet/tx/9705c4f2789a499efb101d12aa37e9f76d09b69250df61e6629ee6318e710a97) |

These two runs used XLM. They predate the USDC-first decision. The USDC flow is in the proof of concept rebuilt on 20 October 2026. Test runs of the rebuilt flow on 20 October 2026, received by the Genghis testnet account `GAMXQ2KPDSVCBU7VCRJROBOUT3RM2VMIVCXVMAW3EYZKBO7TJEYBG4NN`:

| Payment | Order memo | Transaction |
|---|---|---|
| 11.16 USDC, direct payment of USDC | GX100000003 | [1008ba8a...abf5da](https://stellar.expert/explorer/testnet/tx/1008ba8a99ab18d6ea502fe719484508427321f3f11edb326b9eb4dc52abf5da) |
| 5.08 USDC, paid from XLM through the Stellar DEX | GX172022989 | [d8df7af8...fcd86f](https://stellar.expert/explorer/testnet/tx/d8df7af897dfb253868626fc5d54805fbcd2b1beee6966aeff51efcb82fcd86f) |
| 429.08 XLM, Amazon US 75 USD at the live XLM rate | GX434530360 | [1a6b10da...8a5b52](https://stellar.expert/explorer/testnet/tx/1a6b10da4a4b1230c0e336d132e2c71b3ade68756a6255673078c6aec38a5b52) |

Each settled in about five seconds and was matched to its order by memo, asset and amount.

## GRANT: what does not exist yet

| Deliverable | Status |
|---|---|
| Stellar payment path in the production order system (testnet then mainnet) | GRANT |
| Checkout with Stellar Wallets Kit inside genghis.pro | GRANT |
| Payment listener tied to the order state machine, returning the code in the purchase response | GRANT |
| x402 endpoint and memo bridge for agents, with a proposed memo extension to the x402 Stellar scheme | GRANT |
| Spending caps, idempotent requests, monitoring and a threat model | GRANT |
| Open source bridge and merchant adapter for other Stellar merchants | GRANT |

The budget and milestones are in the Interest Form. Architecture: [ARCHITECTURE.md](../ARCHITECTURE.md).

## Repositories and media

| Item | Link |
|---|---|
| Architecture and these pages | https://github.com/genghisecommerce/genghis-stellar-docs |
| Stellar proof of concept | https://github.com/genghisecommerce/genghis-stellar-poc |
| Read-only MCP server | https://github.com/genghisecommerce/genghis-mcp-readonly |
| Payment evidence | https://github.com/genghisecommerce/genghis-payment-evidence |
| Demo video | **[Video URL: to add. A 47 second silent cut exists, a voiceover version is being recorded.]** |

## Sources

- Repositories above, state of 20 October 2026.
- Stellar testnet (Horizon) records for the two transactions, read 20 October 2026.
- Internal build records for the checkout, purchase limits and languages.
