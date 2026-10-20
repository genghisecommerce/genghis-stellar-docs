# 3. Payment activity

Between 3 October 2025 and 20 September 2026 Genghis settled 1,395 crypto payments worth $106,879, from customers who paid with 37 different asset codes (about 20 distinct coins). Every payment is published, anonymised, in a public repository. Status: LIVE, all through a third-party payment processor. None of it is on Stellar.

## Headline

| Metric | Value | Period | Source |
|---|---|---|---|
| Settled payments | 1,395 | 3 October 2025 to 20 September 2026 | [genghis-payment-evidence](https://github.com/genghisecommerce/genghis-payment-evidence) |
| Settled value (payment volume) | $106,879 | Same | Same |
| Asset codes customers paid with | 37 (about 20 distinct coins; a code is a coin plus its network) | Same | Same |
| Payments excluded from totals | 13 flagged as settled far below the invoice, 23 partially paid, 3 with no reliable USD value | Same | Same |

Payment volume is not retail sales. Page 2 explains retail sales. The next sections explain why the two differ.

## Definition of payment volume

- Source: the payment processor's own export, status "finished".
- USD value: the settled amount when the payment settled in a stablecoin (USDT or USDC on any network). For any other settlement asset, the USD value of the invoice.
- Covers every customer type: retail, large buyers, the December 2025 campaign, and any internal or test payment that settled.
- The repository keeps whole dollars only and removes wallet addresses, transaction hashes, order IDs and exact crypto amounts, so a payment cannot be tied back to a customer's wallet. The complete export with transaction hashes is available to reviewers on request: claudio@genghis.pro.
- Recompute: `python3 summarize.py` in the repository rebuilds the monthly totals from `payments.csv`.

## Payments by month

| Month | Settled payments | Settled value |
|---|---|---|
| October 2025 | 57 | $1,252 |
| November 2025 | 123 | $4,650 |
| December 2025 | 371 | $8,792 |
| January 2026 | 92 | $5,727 |
| February 2026 | 54 | $12,290 |
| March 2026 | 87 | $19,760 |
| April 2026 | 24 | $1,677 |
| May 2026 | 38 | $1,081 |
| June 2026 | 92 | $10,886 |
| July 2026 | 99 | $12,798 |
| August 2026 | 151 | $15,750 |
| September 2026, 1 to 20 | 207 | $12,216 |
| Total | 1,395 | $106,879 |

The repository stops at 20 September 2026. The processor's own totals for the full month of September 2026 were $41,993 on 335 payments (processor export of 10 October 2026, same method, large-buyer payments included). A refreshed repository is planned and will be linked here.

## Assets used

By the asset the customer paid with, share of settled value in the repository:

| Asset family | Payments | Value | Share |
|---|---|---|---|
| USDT (all networks; Tron is the largest) | 423 | $61,301 | 57.4% |
| USDC (all networks) | 385 | $15,067 | 14.1% |
| Bitcoin | 98 | $12,091 | 11.3% |
| Monero | 92 | $8,266 | 7.7% |
| Solana | 61 | $2,530 | 2.4% |
| Ethereum | 64 | $2,317 | 2.2% |
| Algorand | 54 | $1,881 | 1.8% |
| Litecoin | 88 | $1,254 | 1.2% |
| Other coins and network variants | 130 | $2,172 | 2.0% |

The processor settles to Genghis in a stablecoin. By value, 88% of settlements were in USDT and 10% in USDC. 326 of the 1,395 payments settled in USDC on Algorand, mostly from the December 2025 Algorand co-marketing campaign.

Stellar is not in this table. Genghis has never accepted a payment on Stellar in production. The Stellar work is described on page 6.

## Why payment volume differs from retail sales

Payment volume for December 2025 to August 2026 (nine complete months) is $88,761. Net sales for all customers in the same months, from the order system, are $138,519. Retail sales are $46,072. Three different numbers, all correct. The bridge:

| Step | Amount |
|---|---|
| Net sales, all customers, December 2025 to August 2026 (order system) | $138,519 |
| Less large-buyer orders settled directly between wallets, outside the processor, March to June 2026 (about) | minus $51,550 |
| Net sales that went through the processor | $86,969 |
| Payment volume in the repository for the same months | $88,761 |
| Payments above order value | $1,792 (2.0%) |

The June part of the $51,550 is approximate, because the large buyer moved onto the processor on 29 June 2026. The $1,792 is processor-side differences: overpayments and rounding by customers, internal test payments and flagged fraud payments that the processor settled but that are not retail orders, and refunded orders. It is not itemised per payment.

The $86,969 that went through the processor splits into:

| Group | Amount, December 2025 to August 2026 | Why it is or is not retail |
|---|---|---|
| Retail sales | $46,072 | Ordinary customers. This is the figure on page 2. |
| Large-buyer orders paid through the processor | $35,902 | A handful of very large orders from four account groups. Real sales, shown separately and excluded from retail so they do not hide ordinary customer behaviour. |
| Algorand campaign, 15 to 22 December 2025 | $4,995 | One-off co-marketing campaign with a different customer mix (average order $18). |
| Total | $86,969 | |

Periods that are not in the bridge:

- October and November 2025: payment volume $5,902. Retail orders recorded for November 2025: $3,115 (18 orders). October 2025 has no retail row.
- 1 to 20 September 2026: payment volume $12,216 in the repository. Retail sales for the whole month were $24,646, so the partial month cannot be compared.

## Order to payment reconciliation, 1 September 2026

An order-level match of processor payments to WooCommerce orders was run on 1 September 2026. It matched 748 payments to orders. Processor payments with no matching order: 181, worth $10,921. Orders with no matching payment: 178, worth $61,566; the largest are the large-buyer orders settled outside the processor. For August 2026 alone, the processor settled 3.8% more than net sales: $15,750 against $15,161.

That match has not been rerun since 1 September. A refreshed reconciliation has not been run since and is open work.

## Methodology and limits

- The repository is built by a script from the processor's exports, de-duplicated by payment ID. The repository carries the output and `summarize.py` to recompute the totals.
- Whole-dollar rounding means monthly totals can differ from the processor's own totals by a few dollars.
- This page does not describe the processor's fee. Net cost of collecting payments is on page 2 (0.5% to 0.76% of sales in August to October 2026).
- Large-buyer orders settled outside the processor are not in the repository and cannot be shown there. They are in the order system.

## Sources

- [genghis-payment-evidence](https://github.com/genghisecommerce/genghis-payment-evidence): `data/payments.csv`, `data/monthly_summary.csv`, `README.md`.
- Management dashboard rebuild of 19 October 2026 (monthly order-system totals) and processor export of 10 October 2026 (September total).
- Order to payment reconciliation of 1 September 2026 (internal).
