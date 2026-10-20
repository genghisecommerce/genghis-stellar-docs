# 5. Conversion problem

About 45% of the customers who start checkout on genghis.pro do not pay. That has improved from 69% in June 2026, and it is still the largest leak in the funnel. This is the problem the grant targets. Status: measured on LIVE checkout; the Stellar fix is TESTNET and GRANT.

## What is measured

**Checkout started to paid**, per window, on WooCommerce order records:

- A customer "started" when they created at least one order in the window. An order is created the moment checkout begins.
- A customer "completed" when at least one of those orders was paid, even if paid after the window closed.
- Unit: distinct customers, identified by billing email, not order rows. Retail only: large-buyer, internal, fraud and campaign orders are excluded.
- Read on 17 October 2026 from the order file of 16 October 2026.

Order rows give lower numbers than customers, because one customer often creates several orders in one visit. We use customers.

| Window | Customers who started | Customers who paid | Started to paid | Did not pay |
|---|---|---|---|---|
| June 2026 | 161 | 50 | 31.1% | 68.9% |
| 1 to 23 July 2026 | 190 | 64 | 33.7% | 66.3% |
| 15 to 24 August 2026 | 132 | 40 | 30.3% | 69.7% |
| 25 to 31 August 2026 (in-house checkout live from 25 August) | 101 | 31 | 30.7% | 69.3% |
| 1 to 30 September 2026 | 476 | 214 | 45.0% | 55.0% |
| 14 to 20 September 2026 | 123 | 62 | 50.4% | 49.6% |
| 21 to 27 September 2026 | 114 | 64 | 56.1% | 43.9% |
| 28 September to 4 October 2026 | 173 | 96 | 55.5% | 44.5% |
| 5 to 11 October 2026 | 181 | 98 | 54.1% | 45.9% |
| 12 to 17 October 2026 | 113 | 63 | 55.8% | 44.2% |
| 1 to 17 October 2026 | 371 | 195 | 52.6% | 47.4% |

Reading the table:

- Conversion was about 31% from June to the end of August. It rose after the in-house checkout and the releases that followed, to about 55% in the weekly windows since 21 September 2026.
- The latest windows are immature: an order created a few hours ago can still be paid. Their conversion can only go up.
- The earlier windows up to 13 September are measurements taken at the time, not recalculated. Windows from 14 September were recalculated on 17 October.
- We do not attribute the change to a single cause. Several releases overlapped: the in-house checkout (25 August), the German site (8 October), the display-currency setting (9 October) and a first set of checkout releases from 24 September.
- An earlier figure of 35.4% for June, on a different count method, is replaced by 31.1% above.

So the claim is: **about 45% of customers who start checkout still leave without paying**, measured 21 September to 17 October 2026. Earlier materials said "more than half". That was true until mid September and is no longer true.

## Why people leave, from session replay

The following findings come from recorded sessions on the old payment redirect, measured before the in-house checkout. They explain the problem and are not a measure of today's checkout.

| Finding | Value | Sample and period |
|---|---|---|
| Sessions analysed | 37,704 non-bot sessions | Since 24 October 2025 to 17 August 2026, Microsoft Clarity |
| Sessions that reached the pay button and pressed it two or more times | 10% to 26% a month | Every month since December 2025 |
| Wait after paying before the buyer learns whether the order went through | 5 to 24 minutes | Sessions returning from the payment page |
| Sessions where a raw error message replaced the payment screen | 16 confirmed, 10 of them in India, 9 of those on a phone | A floor, not a total, because we only see people who clicked on the error |

Source: internal analysis of 17 August 2026. Only the figures above are published. Clarity session recordings contain customer behaviour and are not public.

## What the payment step asks of a buyer

Paying means copying an address and an exact amount, switching to a wallet, sending, and waiting for confirmations. A buyer who has no wallet connected at that moment has to leave the page. An AI agent cannot do the step at all.

## What the grant would test

- A checkout where the buyer connects a Stellar wallet and signs the payment inside the page. The payment settles in about five seconds, so the code can be returned in the same step. Status: TESTNET proof of concept (page 6), GRANT for production.
- The hypothesis is that removing the copy-address and wait steps lifts started-to-paid conversion. It is a hypothesis, not a result. The measure we will report is the same one used above: customers who started checkout and paid, from order records, per window.
- The Stellar path has not been measured against the current checkout, because it is not in production.

## Sources

- WooCommerce order records, read 17 October 2026, management dashboard rebuild of 19 October 2026 ("checkout truth" table).
- Session replay analysis of 17 August 2026 (internal; the published figures only).
