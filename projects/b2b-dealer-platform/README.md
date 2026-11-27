# B2B dealer purchasing platform

I worked on a B2B purchasing platform where dealers could order directly. It integrated with the company's existing software and used current raw material prices. This case study describes the purchasing workflow and one engineering decision from the .NET backend.

## Why pricing needs context

A price on the storefront, the amount recorded on an order and a total used for reporting answer different questions. The backend models exchange rates explicitly and groups nominal amounts by currency. That distinction matters whenever a dealer works in one currency and another team reviews orders across several currencies.

For example, if one order is for USD 120 and another is for EUR 80, the nominal report shows USD 120 and EUR 80 as separate totals. A single total would require a reporting currency and a known exchange rate. The amounts in this example are illustrative.

## How the project is organised

- **Dealer storefront** — The dealer-facing web application supports the buying workflow.
- **Administration** — A separate panel handles catalogue operations, including the publication queue.
- **.NET backend** — The application layer contains pricing and currency rules. Persistence and ERP integration code live in separate parts of the solution.

## One engineering decision

The exchange-rate snapshot uses USD as its base. It distinguishes an absent rate from a non-positive rate, so a caller can tell missing configuration from an invalid value. Reporting accumulates nominal amounts within each currency before rounding each subtotal. These rules can be exercised independently of a live ERP connection.

The original project contains tests for pricing rules, commercial currency handling and the price snapshot used for ERP export. This public overview uses illustrative data. The company repository, product catalogue and operational configuration are private.
