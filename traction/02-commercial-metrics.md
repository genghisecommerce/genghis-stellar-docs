# 2. Commercial metrics

Retail sales grew from $1,016 in May 2026 to $24,646 in September 2026. October is on a faster path: $30,981 in the first 19 days.

Data covers 1 December 2025 to 19 October 2026. October is a partial month. The series was built on 19 October 2026 from WooCommerce order records. Status: LIVE business, unaudited management information.

## Definitions

Terms are defined on the [landing page](README.md#definitions-used-on-every-page). In short: GMV is paid orders before refunds, net sales is GMV minus refunds, retail sales is net sales from ordinary customers only, and payment volume is what the payment processor settled (page 3).

Retail excludes: orders from four large-buyer account groups, the December 2025 Algorand campaign, internal accounts and flagged fraud. Each exclusion is shown as its own column below so nothing is hidden.

## Monthly retail series

| Month | Retail sales | Retail orders | Average order value | Orders from new customers | Orders from returning customers |
|---|---|---|---|---|---|
| November 2025 | $3,115 | 18 | $173.05 | n/a | n/a |
| December 2025 | $3,685 | 59 | $62.46 | 43 | 16 |
| January 2026 | $6,184 | 74 | $83.57 | 52 | 22 |
| February 2026 | $1,811 | 45 | $40.25 | 32 | 13 |
| March 2026 | $4,099 | 81 | $50.61 | 52 | 29 |
| April 2026 | $1,597 | 21 | $76.03 | 19 | 2 |
| May 2026 | $1,016 | 32 | $31.75 | 23 | 9 |
| June 2026 | $7,289 | 88 | $82.83 | 46 | 42 |
| July 2026 | $9,132 | 90 | $101.47 | 65 | 25 |
| August 2026 | $11,259 | 134 | $84.02 | 112 | 22 |
| September 2026 | $24,646 | 333 | $74.01 | 224 | 109 |
| October 2026, 1 to 19 | $30,981 | 352 | $88.01 | 238 | 114 |

Notes on the table:

- Retail sales are net of refunds. The retail series has no October 2025 row. The first payments of that month (57 payments, $1,252) are in the payment evidence on page 3 and are not reconciled to retail orders.
- November 2025 is from the customer cohort table. It has no new and returning split in the series.
- Average order value is retail sales divided by retail orders. The median purchase is much lower than the average: $26.21 across all purchases, lifetime to 19 October 2026.
- February to May 2026 were weak months in retail. In those months the large-buyer accounts below made most of the sales, and retail was not growing. It started to grow from June.
- A first set of checkout releases went live from 24 September 2026. Several releases overlapped in September, so we do not claim a single cause for the step up.

## What is excluded from retail, by month

| Month | Retail sales | Large-buyer sales | Campaign sales | GMV before refunds, all segments | Refunds | Net sales, all segments |
|---|---|---|---|---|---|---|
| December 2025 | $3,685 | $12 | $4,995 | $8,973 | $282 | $8,690 |
| January 2026 | $6,184 | $393 | $0 | $6,734 | $157 | $6,577 |
| February 2026 | $1,811 | $10,690 | $0 | $12,503 | $2 | $12,501 |
| March 2026 | $4,099 | $20,976 | $0 | $25,095 | $21 | $25,075 |
| April 2026 | $1,597 | $22,068 | $0 | $23,665 | $0 | $23,665 |
| May 2026 | $1,016 | $14,738 | $0 | $15,758 | $4 | $15,755 |
| June 2026 | $7,289 | $11,014 | $0 | $18,305 | $3 | $18,303 |
| July 2026 | $9,132 | $3,660 | $0 | $12,817 | $26 | $12,792 |
| August 2026 | $11,259 | $3,909 | $0 | $16,294 | $1,132 | $15,161 |
| September 2026 | $24,646 | $17,064 | $0 | $42,545 | $835 | $41,709 |
| October 2026, 1 to 19 | $30,981 | $10,599 | $0 | $41,654 | $74 | $41,580 |

Large-buyer sales and retail sales add up to net sales for the months shown, apart from the campaign column in December 2025 and rounding.

Worked example, September 2026, so the four terms can be checked against each other:

| Quantity | Value |
|---|---|
| GMV before refunds, all segments | $42,545 |
| Refunds (7 orders) | $835 |
| Net sales, all segments | $41,709 |
| Less large-buyer sales | $17,064 |
| Retail sales | $24,646 (333 orders) |

Large-buyer sales have been part of the business since February 2026 and are not hidden. They are excluded from retail so that retail shows what ordinary customers do. Over the three closed months July to September 2026, large-buyer sales were 35.4% of net sales. The monthly share was 29% in July, 26% in August and 41% in September.

August 2026 had a refund rate of 6.95% of GMV (17 refunded orders), the highest of any month. Across the whole series there are 60 refunds worth $2,536: 15 supplier-side, 10 our own error, 4 payment problems and 31 not yet classified. Refunds are deducted from every sales figure on this page.

## Customers

Customers are distinct billing emails with at least one paid retail order. Counted from the first sale to 19 October 2026.

| Metric | Value | Definition |
|---|---|---|
| Customers | 802 | Distinct customers, lifetime. |
| Retail orders | 1,327 | Lifetime. |
| Retail sales | $104,813 | Lifetime, net of refunds. |
| Average order value | $78.98 | Lifetime sales divided by orders. |
| Median purchase | $26.21 | Orders placed within 24 hours by one customer count as one purchase. |
| Repeat rate | 17.1% | Customers with two or more purchases, as a share of all customers. |
| Repeat rate, registered customers | 31.4% | Customers with an account. |
| Repeat rate, guest customers | 9.7% | Checked out without an account. |
| Median days to a second purchase | 6 | Of the 137 customers who bought again. |
| Countries by customer home market | 46 | Country with most of the customer's spend. |

The business depends on small first purchases. The median first purchase is $23.31 and the median later purchase is $37.02. Customers who bought once account for 82.9% of customers and 52.0% of retail sales. The 119 customers who bought two to four times account for 35.0%. The 18 customers who bought five or more times account for 13.1%.

## Profitability

Genghis has been net profitable every month since March 2026 (management estimates, unaudited, not statutory accounts). Until July most of the profit came from margin on large-buyer orders; from August retail margin alone covers fixed costs.

| Month | Product margin on retail | Payment collection cost | Gross profit, all segments | Net profit after fixed costs |
|---|---|---|---|---|
| August 2026 | 4.62% | 0.76% | $644 | +$211 |
| September 2026 | 5.16% | 0.62% | $1,894 | +$1,461 |
| October 2026, 1 to 19 | 4.64% | 0.50% (assumed) | $1,729 | +$1,296 after a full month of fixed costs |

- Fixed costs are about $430 a month in the model (hosting, tools and similar). This estimate is under review.
- Net profit above includes margin earned on large-buyer orders.
- Retail alone has covered the fixed costs since August 2026. Retail contribution margin was 4.54% in September 2026, which is about $1,119 on $24,646. The retail break-even is about $9,300 of retail sales a month. Retail sales were above it in August, September and October, and just below it in July ($9,132).
- Margin is low by design. Genghis charges no platform fee. Its margin is the spread between the supplier price and the price the customer pays. Every margin figure is margin on sales, not markup.
- Net profit in earlier months, from the same model: December 2025 minus $359, January minus $358, February minus $194, March plus $134, April plus $836, May plus $451, June plus $763, July plus $155. Most of March to July came from margin on large-buyer orders. Margins before April 2026 are assumptions. Measured margins start in April.
- This page does not claim the company is profitable on a statutory basis. The first statutory accounts are due 14 December 2026.

## Methodology

- Source of truth for sales: WooCommerce paid orders. Web analytics is a partial purchase signal and is not used for revenue.
- Segmentation: one function in the management dashboard decides whether an order is retail, large-buyer, campaign, internal or fraud. Internal test accounts and flagged fraud orders are excluded from every figure on this page.
- Margin per order is measured against the supplier price at the time of the order.
- Refunds come from the order records and are shown by month.
- Net sales for August 2026 read $15,161 in the refund table and $15,168 in the monthly summary of the same rebuild. The refund table is used here.
- Rebuild date: 19 October 2026. The figures for earlier months can move by small amounts when refunds post later. For example June 2026 reads $7,289 here and $7,334 in an earlier version of the form.

## Sources

- WooCommerce order records, processed by the management dashboard rebuild of 19 October 2026.
- Customer and cohort tables from the same rebuild.
- Finance notes, September and October 2026 (internal).
