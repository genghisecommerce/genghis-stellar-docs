# Genghis: traction and supporting evidence

Prepared for the Stellar Community Fund Interest Form, 20 October 2026. Every number on these pages has a definition, an exact period, a source and, where it can be public, a link. Where a number could not be verified it is not here.

Genghis (genghis.pro) is a live marketplace run by Genghis Ltd, a UK company (number 16315448). It sells gift cards, eSIMs, mobile top-ups and game keys, paid in crypto.

## What is live, what is testnet, what the grant funds

Each page labels its content with one of three status tags.

| Tag | Meaning |
|---|---|
| LIVE | Running on genghis.pro today, with real customers and real money. |
| TESTNET | Running on Stellar testnet as a proof of concept. No real money moves. |
| GRANT | Does not exist yet. The grant would fund it. |

Nothing on Stellar mainnet is live today. Genghis does not yet accept any payment on Stellar in production.

## Data dates

| Dataset | Covers | Read on |
|---|---|---|
| Commercial metrics (WooCommerce orders, management dashboard) | 1 December 2025 to 19 October 2026 (October is a partial month) | Built 19 October 2026 |
| Payment evidence (processor export, public repository) | 3 October 2025 to 20 September 2026 | Published September 2026 |
| Catalogue (WooCommerce catalogue and public catalogue API) | Snapshot | 20 October 2026 |
| Checkout conversion (WooCommerce orders) | 1 June to 17 October 2026 | Read 17 October 2026 |

## Definitions used on every page

Four different quantities are easy to confuse. We keep them apart.

| Term | Definition | Includes | Excludes |
|---|---|---|---|
| Payment volume | The USD value of crypto payments that the payment processor marks as finished. | Every customer type, tests that settled, orders later refunded. | Partial payments, payments with no reliable USD value. |
| GMV (gross merchandise value) | The value of paid orders on genghis.pro as charged to the customer, before refunds. We use GMV and "gross sales" as the same quantity. | Retail, large-buyer, campaign and refunded orders. | Internal test orders, flagged fraud orders, unpaid orders. |
| Net sales | GMV minus refunds. | As above, after refunds. | Refunded value. |
| Retail sales | Net sales from ordinary customers only. This is the figure the form calls "retail revenue". | Orders from ordinary customers, net of refunds. | Large-buyer orders (four account groups), the December 2025 Algorand campaign, internal accounts, flagged fraud. |
| Gross profit | Sales minus the cost of the goods and the payment collection cost. Genghis sells as principal, so the full sale is its turnover and the margin is the gross profit. | Margin measured per order against the supplier price. | Fixed costs. |

Why retail excludes some orders: a handful of very large orders would otherwise hide what ordinary customers do. Large-buyer orders are real sales and are shown separately wherever they matter. Source of the rule: the retail segmentation function used by the management dashboard. WooCommerce, our order system, is the source of truth for sales. Web analytics is not used for revenue.

All amounts are USD. All figures are management information. They are not audited. Genghis Ltd files its first statutory accounts with Companies House by 14 December 2026.

## Figures at a glance

| Metric | Value | Period | Page |
|---|---|---|---|
| Retail sales | $24,646 from 333 orders | September 2026 | [Commercial metrics](02-commercial-metrics.md) |
| Retail sales, partial month | $30,981 from 352 orders | 1 to 19 October 2026 | [Commercial metrics](02-commercial-metrics.md) |
| Customers, lifetime | 802 | 3 October 2025 to 19 October 2026 | [Commercial metrics](02-commercial-metrics.md) |
| Customers who bought more than once | 17.1% | Lifetime to 19 October 2026 | [Commercial metrics](02-commercial-metrics.md) |
| Settled crypto payments | 1,395 worth $106,879 | 3 October 2025 to 20 September 2026 | [Payment activity](03-payment-activity.md) |
| Crypto assets customers paid with | 37 | Same period | [Payment activity](03-payment-activity.md) |
| Products in stock | 4,506 of 6,258 listed | 20 October 2026 | [Product adoption](04-product-adoption.md) |
| Countries with a product in stock | 86 | 20 October 2026 | [Product adoption](04-product-adoption.md) |
| Checkout started to paid | 52.6% (371 customers started) | 1 to 17 October 2026 | [Conversion problem](05-conversion-problem.md) |
| Net profit, management estimate | Positive every month | March to October 2026 | [Commercial metrics](02-commercial-metrics.md) |

## Pages

1. [Company and operating history](01-company.md)
2. [Commercial metrics](02-commercial-metrics.md)
3. [Payment activity](03-payment-activity.md)
4. [Product adoption](04-product-adoption.md)
5. [Conversion problem](05-conversion-problem.md)
6. [Product delivery](06-product-delivery.md)
7. [Programmes and recognition](07-programmes-and-recognition.md)
8. [Community and distribution](08-community-and-distribution.md)
9. [Media and content](09-media-and-content.md)
10. [Events and ecosystem activity](10-events-and-ecosystem.md)
11. [Partnerships and suppliers](11-partnerships-and-suppliers.md)
12. [Team credibility](12-team.md)

## Public repositories

- [genghis-payment-evidence](https://github.com/genghisecommerce/genghis-payment-evidence): every settled payment, anonymised.
- [genghis-mcp-readonly](https://github.com/genghisecommerce/genghis-mcp-readonly): read-only catalogue server for AI agents.
- [genghis-stellar-docs](https://github.com/genghisecommerce/genghis-stellar-docs): architecture and these pages.
- [genghis-stellar-poc](https://github.com/genghisecommerce/genghis-stellar-poc): the Stellar testnet proof of concept. Live at https://genghisecommerce.github.io/genghis-stellar-poc/

Questions or a request for the full payment export: claudio@genghis.pro.
