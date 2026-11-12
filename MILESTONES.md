# Genghis on Stellar: milestones and budget

Three tranches from December 15, 2026 to March 31, 2027. Total budget: $88,000 (tranche 1: $28,100; tranche 2: $39,200; tranche 3: $20,700). Components carry the names used in the architecture.

---

## Tranche 1: Stellar core: Stellar Wallets Kit implemented ($28,100)

### 1.1 Stellar settlement account (USDC) and Stellar payment path in the order system

**Description.** Genghis account on Stellar testnet with a USDC trustline and separate signers (outgoing payments kept apart from the web servers). Every order settles in USDC: the order system issues the payment request (USDC amount, unique text memo, expiry in `timeBounds`) and extends the order state machine (`created` to `refund due`, `refunded`). Reconciliation matches on the expected memo or hash, asset, issuer and amount; a payment that cannot be tied to an order is never delivered.

**How to measure completion.**
- On testnet, a USDC payment carrying a valid memo is attributed to its order and moves it to `paid`.
- A payment with no memo, an unknown memo, XLM sent directly or an insufficient amount is held and not delivered.
- The failure-path test suite is public in the repository and runs in CI.

**Budget.** $8,800

**Delivery date.** December 26, 2026

### 1.2 Stellar Wallets Kit checkout

**Description.** Stellar Wallets Kit v2 in the genghis.pro checkout on staging, against the real catalogue: connection (e.g., Freighter, xBull, LOBSTR), mobile through WalletConnect, USDC shown first, signing inside the page. A buyer holding XLM or EURC signs a `pathPaymentStrictReceive` that delivers the exact USDC amount in one transaction, with no conversion on the Genghis side. A buyer without a Stellar wallet keeps the current checkout.

**How to measure completion.**
- A complete purchase on testnet from the staging storefront, signed with at least two wallets from the kit including one mobile wallet through WalletConnect, code delivered.
- The path payment cases from XLM and from EURC are recorded with their hashes.
- The current checkout is unchanged for every other buyer.

**Budget.** $6,700

**Delivery date.** January 3, 2027

### 1.3 Payment listener, synchronous delivery and Genghis Purchase API v1

**Description.** Listener inside the order system: Horizon payment stream of the Genghis account, Stellar RPC `getEvents` on the USDC contract as a second source, persistent cursor and catch-up on restart; the code is returned in the purchase response as soon as the payment settles. REST API authenticated by integrator key and rate-limited: create an order and receive the Stellar payment request (and the unsigned transaction XDR), track its state, read the code once, declare a return account. This is the surface the checkout, the SDK, the x402 endpoint and partners use.

**How to measure completion.**
- On testnet, an order is delivered and the code returned in the same response after settlement.
- A transfer issued by a contract (SAC `transfer`) is seen by the second source and reconciled.
- Restarting the listener in the middle of a payment loses and duplicates no order (public test).
- The OpenAPI specification is public; a reference client creates an order, signs the supplied XDR with a testnet account and receives the code, readable once.

**Budget.** $12,600

**Delivery date.** January 18, 2027

---

## Tranche 2: every path exercised: CCTP, Near Intents, Axelar and Soroswap implemented, Stellar Wallets Kit extended ($39,200)

### 2.1 x402 endpoint for agents: Stellar and CCTP chains, CCTP repatriation service

**Description.** Endpoint on the x402 `exact` scheme (`x402Version` 2), replacing our custom XLM and memo prototype. The 402 response names `stellar:testnet` first, with USDC and the Genghis account as `payTo`, then one `accepts` entry per CCTP-covered chain where a facilitator settles (e.g., Base, Ethereum, Arbitrum, Solana), each towards a Genghis account on that chain; OpenZeppelin's Build on Stellar Relayer verifies and settles, with AgentSmith as the alternative. Per-order and per-session caps, idempotency, server-set price; discovery through the existing MCP server. The CCTP repatriation service, one service for every chain (EVM and Solana adapters), burns the USDC held on the receiving accounts (`depositForBurnWithHook`, destination 27) with `mintRecipient` and `destinationCaller` set to the `CctpForwarder` and the Genghis Stellar account in the `hookData`, reads the Iris attestation and calls `mint_and_forward`; 6/7 decimal conversion to message units; the listener waits for the mint hash.

**How to measure completion.**
- Agent purchases run by the team with a standard x402 client are delivered on Stellar testnet and from two source testnet chains (e.g., Base Sepolia and Sepolia), logs and hashes recorded.
- A request above the cap is refused; a repeated request returns the first result without a second payment.
- The matching repatriation lands on the Genghis Stellar testnet account, burn hash and mint hash published.
- A public unit test covers the `hookData` encoding byte by byte and the rejection of an invalid address.

**Budget.** $14,800

**Delivery date.** February 5, 2027

### 2.2 Near Intents intake

**Description.** 1Click quote (`POST /v0/quote`) with USDC on Stellar as destination and the Genghis account as recipient, deposit address shown to the buyer, intent tracked through to the Stellar delivery hash, reconciliation on that hash, refund address for the failure cases; enrolment in the partner programme. Below the Near Intents per-chain minimums, the checkout keeps the current processor.

**How to measure completion.**
- Dry quotes are recorded for at least three origin assets (e.g., BTC, ETH, USDT).
- Two real swaps of a few dollars to the Genghis mainnet account are delivered and reconciled, hashes published (Near Intents has no testnet).
- An expired quote produces a new quote and a new address; an order below the minimum is routed to the processor (public tests).

**Budget.** $5,300

**Delivery date.** February 11, 2027

### 2.3 Axelar conversion executor (Soroban) and Soroswap conversion

**Description.** A Soroban contract that receives a token through Axelar's Interchain Token Service (`InterchainTokenExecutable` macro), checks the authorized source chain and address, converts it to USDC through `swap_exact_in` on Soroswap's Aggregator v3 contract (fixed address, never supplied by the caller) with `min_out` and per-token configured routes, deposits the USDC on the Genghis account and emits an event carrying the reference; on failure or slippage, the token goes to the return queue, with no delivery. The contract builds on OpenZeppelin `stellar-contracts` 0.8.0 (`Ownable`, `Pausable`, `Upgradeable`). A token is only enabled if a real $1,000 quote from the Aggregator API shows a spread under 1% all fees included. The contract source is public under a permissive licence from the first testnet deployment.

**How to measure completion.**
- On testnet, an ITS transfer with payload triggers the conversion and the deposit of USDC on the Genghis account, hashes published.
- A swap whose minimum received cannot be met ends in the return queue, with no delivery (public test).
- Executor unit tests against mainnet resource limits, authorization assertions and fuzzing on amounts in the repository; Scout (CoinFabrik) static analysis run published, no open high finding.

**Budget.** $10,600

**Delivery date.** February 24, 2027

### 2.4 Outgoing payments service, sanctions screening, monitoring plan and threat model

**Description.** Outgoing payments service with a dedicated signer kept off the web servers, daily cap, two-person approval above a threshold, a log linking each order to its hash; USDC refunds for every case of the state machine, a `pathPaymentStrictSend` from USDC for a buyer with no USDC trustline who paid from XLM or EURC, ITS return of queued tokens; sender screening before delivery through a specialised provider (e.g., Chainalysis); monitoring plan (unreconciled payments, listener lag, balances, refund and return queues, attestations, intents, executor) and STRIDE threat model published; extended kit wallet matrix (e.g., Albedo, Hana, Rabet) published.

**How to measure completion.**
- Every case of the state machine produces its refund transaction on testnet, listed with its hash, including a path payment refund to an account with no USDC trustline.
- An ITS return from the queue is executed on testnet.
- A listed test sender is blocked before delivery.
- The monitoring plan and the threat model are public in the documentation repository, each threat tied to a mitigation or an accepted residual risk.
- An injected event (unreconciled payment) fires its alert.
- Every wallet in the matrix completes a testnet purchase.

**Budget.** $8,500

**Delivery date.** March 6, 2027

---

## Tranche 3: mainnet: Stellar Wallets Kit, CCTP, Near Intents, Axelar and Soroswap in production ($20,700)

### 3.1 Mainnet launch of the Stellar checkout

**Description.** Genghis mainnet account with its USDC trustline and signers, Stellar Wallets Kit live in the genghis.pro checkout, Purchase API, listener, outgoing payments, screening and monitoring in production; XLM through the processor enabled as a secondary option (a processor setting, outside the budget). The account address is published: adoption is read from it.

**How to measure completion.**
- Purchases run by the team on mainnet through the kit, including one paid from EURC and one from XLM through a path payment and one from a mobile wallet through WalletConnect, hashes and references published.
- A refund executed on mainnet with its hash.
- Monitors live, alert channel documented.

**Budget.** $8,300

**Delivery date.** March 16, 2027

### 3.2 Agent and cross-chain paths in production

**Description.** x402 endpoint on `stellar:pubnet` with OpenZeppelin's Build on Stellar Relayer as the production facilitator (AgentSmith as the alternative) and the CCTP chains enabled; CCTP repatriation service in production (mainnet contracts, domain 27); Near Intents intake open; Axelar conversion executor deployed on mainnet with a SEP-55 verified build (metadata, GitHub attestation, release WASM), for the tokens that pass the activation rule.

**How to measure completion.**
- One agent purchase per path (x402 Stellar, x402 on a CCTP chain + repatriation, Near Intents, Axelar + Soroswap) run by the team on mainnet, hashes published.
- Executor contract ID published with its verified-build page.
- A mainnet CCTP repatriation with burn and mint hashes.

**Budget.** $6,700

**Delivery date.** March 24, 2027

### 3.3 Genghis Checkout SDK 1.0 and wallet integration guide

**Description.** TypeScript SDK published on npm (permissive licence): builds the Stellar transaction that delivers USDC (direct payment, or path payment from EURC or XLM), hands it to the host wallet for signing, tracks settlement, returns the code. Integration guide for a wallet or an application ("spend" tab, end of a received transfer) and public reference application.

**How to measure completion.**
- Package published with a release tag and a public repository.
- The reference application completes an end-to-end mainnet purchase from a team account, hash published.
- The integration guide is public and covers the failure cases of the state machine.

**Budget.** $5,700

**Delivery date.** March 31, 2027

---

## Tranche #3 Onchain Metric Information

**1. What metric do you plan to measure (must be NAV, volume, or something similar)?** Orders settled in USDC on the published Genghis Stellar account, by people or agents, whatever the path (direct payment or path payment from a wallet, x402 on Stellar, Near Intents, Axelar and Soroswap): number of distinct paying wallets, number of settled orders, cumulative USDC volume. Team accounts are excluded.

**2. What is your completion target?** At least 50 distinct paying wallets and at least 100 orders settled in USDC between the mainnet launch of the checkout (deliverable 3.1) and the tranche 3 submission, cumulative volume reported.

**3. How will you track and report it?** The account address is published in the documentation repository; every settled order is tied to its transaction hash in the payment log; the tranche report gives the three figures with the list of hashes and the link to the account on a public explorer (e.g., Stellar Expert), verifiable without authentication.
