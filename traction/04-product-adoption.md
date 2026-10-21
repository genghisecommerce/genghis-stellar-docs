# 4. Product adoption

Genghis has 4,506 products in stock out of 6,258 listed, across 86 countries. This page fixes one definition of "catalogue" and uses it everywhere. Status: LIVE.

## One definition

**A product is one product page on genghis.pro: one brand in one country market, with every value (denomination) selectable on the same page.** For example "Amazon US" is one product with many values. "Amazon UK" is a different product.

Genghis counts products, not brands. There is no brand field in the catalogue, so a brand count would be an estimate. Earlier materials used "4,000+ gift card brands" and "5,719 products". Both are replaced by the counts below.

| Term | Meaning | Count, 20 October 2026 |
|---|---|---|
| Products listed | Published product pages | 6,258 |
| Products in stock | Published and at least one value available | 4,506 |
| Headline figure | In-stock count rounded down | 4,500+ products |

Measured on 20 October 2026 through the public catalogue API that the read-only MCP server uses, so anyone can repeat it. The WooCommerce admin count on the same day was 6,278 listed and 4,514 in stock. The difference of 20 listed products is items with no country assigned.

## Catalogue by product type

| Type | Listed | In stock |
|---|---|---|
| Gift cards and vouchers | 5,200 | 3,864 |
| Game keys | 693 | 399 |
| Mobile top-ups and payments | 241 | 139 |
| Prepaid cards | 70 | 50 |
| eSIMs | 54 | 54 |
| Total | 6,258 | 4,506 |

Type is the product's category. Every product is delivered digitally.

## Brands, if a brand number is needed

- No brand field exists. The brand taxonomy has 28 terms and 464 tagged products.
- An estimate from product names, with country, currency and denomination stripped, gives about 3,000 distinct brand names in stock when game keys are excluded (game keys are named by title, not by brand). The method is approximate, with an error of roughly 10%.
- We do not use a brand number in the headline for that reason.

## Countries

| Metric | Value | Method |
|---|---|---|
| Countries with at least one product in stock | 86, plus worldwide products | Country tags on products, public catalogue API, 20 October 2026 |
| Country markets with at least one listed product | 92 | Same |
| Worldwide products (not tied to a country) | 365 in stock | Same |
| Country markets with more than 100 listed products | 50 | Same |

Largest markets by number of listed products: United States 522, Germany 385, United Kingdom 325, France 312, United Arab Emirates 267, Brazil 267, Italy 239, Indonesia 225, Sri Lanka 222, Netherlands 216. Worldwide products: 592 listed.

Customers bought from 46 countries by home market, counted to 19 October 2026. Top home markets by customers: United States 26.9%, India 13.3%, Turkey 6.4%, France 3.0%, United Kingdom 2.9%, Germany 2.5%. 17.5% of customers bought only worldwide products and have no single home market.

## Emerging-market share

We report three measures. They differ because they answer different questions.

| Measure | Value | Date | Method |
|---|---|---|---|
| Catalogue: in-stock products that serve only emerging markets | 37.1% (1,673 of 4,506) | 20 October 2026 | A product counts when every country it serves is outside the high-income list below. Worldwide products and products with no country stay in the denominator. |
| Catalogue: same, among country-specific products | 40.6% (1,673 of 4,121) | 20 October 2026 | Worldwide and unassigned products removed from the denominator. |
| Customers whose home market is emerging | 30.8% (250 of 812) | To 21 October 2026 | Home market is the country with the most of the customer's spend. |
| Retail sales from customers with an emerging home market | 22.1% ($23,882 of $108,118) | To 21 October 2026 | Same. 85.3% of sales could be assigned to a market. |

Emerging means any country not on this high-income list: United States, United Kingdom, Canada, Australia, New Zealand, Japan, South Korea, Singapore, Hong Kong, Taiwan, Israel, Switzerland, Norway, Iceland, Ireland, Germany, France, Italy, Spain, Portugal, the Netherlands, Belgium, Luxembourg, Austria, Denmark, Sweden, Finland, Greece, Cyprus, Malta, Slovenia, Slovakia, Czech Republic, Estonia, Latvia, Lithuania, Poland, Croatia, the United Arab Emirates, Qatar, Kuwait, Saudi Arabia, Bahrain, Monaco, Liechtenstein, Andorra and Europe as a region.

Gulf states are on the high-income list. Counting them as emerging would raise the catalogue share.

An earlier version of the form said 47% of the catalogue serves emerging markets. That figure was measured on 6 August 2026 with a method we could not reproduce, so it is retired.

Where emerging-market customers are largest: India (107 customers, 13.3% of customers, 12.9% of sales), Turkey (51 customers, 6.4%), the Philippines (10 customers). Customers in India repeat more than the lifetime average: 25.2% against 17.1%.

## Languages of the storefront

English, German (live 8 October 2026), Spanish (11 October 2026) and Turkish (13 October 2026). The Help Center has 145 English articles, 145 in German and Spanish, and 138 in Turkish (13 October 2026).

## Methodology

- Catalogue counts: public GraphQL catalogue endpoint of Genghis, read on 20 October 2026, 63 pages of 100 products. Read-only. Product type from the product's category. Country from the product's country tag.
- Customer geography: the management dashboard customer model, rebuild of 19 October 2026. Definitions are on page 2.
- Not a measure of what is bought. Catalogue share says what Genghis offers. Customer and sales shares say what customers bought.

## Sources

- Public catalogue API, read 20 October 2026: https://be.genghis.pro/wc-shop/graphql
- WooCommerce catalogue count, read 20 October 2026 (admin API, read-only).
- Management dashboard rebuild of 19 October 2026 (customer geography).
- [genghis-mcp-readonly](https://github.com/genghisecommerce/genghis-mcp-readonly): the `list_countries` and `search_products` tools read the same data.
