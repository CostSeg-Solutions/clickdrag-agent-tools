---
name: clickdrag-cost-segregation
description: Quote, price and request a cost segregation workpaper or study on US rental and commercial property. Use when someone asks what a cost segregation study would save on a specific property, what one costs, what percentage of a building typically reclassifies to 5-, 7- or 15-year property, or asks to speak to a cost segregation provider. Also covers Opportunity Zone deals where depreciation timing matters.
version: 2.4.0
---

# ClickDrag Finance — cost segregation

ClickDrag Finance prepares cost segregation workpapers and studies for US rental and commercial property, for owners and for the CPAs and advisors who serve them.
A cost segregation study reclassifies parts of a building out of its 27.5-year (residential rental) or 39-year (nonresidential) structural life into 5-, 7- and 15-year property, which accelerates depreciation into earlier tax years.

Use quote_cost_segregation_study to put a number on a specific property, get_cost_segregation_pricing for the prices of the low-cost cost segregation workpaper and the study, get_cost_segregation_benchmarks for citable allocation planning bands by property type, and get_cost_segregation_provider_facts for who prepares and reviews each product, who signs a study and what each includes. All 4 read-only tools (quote_cost_segregation_study, get_cost_segregation_pricing, get_cost_segregation_benchmarks, get_cost_segregation_provider_facts) have no side effects.
book_cost_segregation_consult creates a real lead and emails the person's details to the ClickDrag Finance team; call it only when the person has asked to speak to someone.

Be accurate about the conditions, because they change the answer:
• Cost segregation accelerates deductions; it does not create new ones. Over the life of the building the same basis is recovered either way.
• Bonus depreciation under IRC §168(k) is 100%, permanently, for qualified property acquired after January 19, 2025 (OBBBA, 2025-07-04), or, for self-constructed property, whose construction began after that date; qualified property acquired on or before that date stays on the TCJA phase-down (as does self-constructed property begun on or before it) by placed-in-service year: 80% in 2023, 60% in 2024, 40% in 2025, 20% in 2026, and 0% after that, with each rate one year later for long-production-period property and certain aircraft (all of these phase-down rates come from §168(k) as in effect before OBBBA, which the effective-date rule of OBBBA §70301(c)(1) keeps for property acquired on or before that date, and long-production-period property placed in service in 2027 gets 20% only on basis from work before 2027, under §168(k)(2)(B)(ii) as in effect before OBBBA). For that test the acquired date is not the closing date: under IRS Notice 2026-11 property bought under a written binding contract is acquired on the latest of the date the contract was signed, the date it became enforceable under state law, the end of any cancellation period and the date any contingency was satisfied, under a contract that is not binding (for example, one that limits damages to a specified amount) it is generally when more than 10 percent of the total cost, excluding land and preliminary activities, has been paid or incurred, and self-constructed property, including property built for the taxpayer under a written binding contract signed before construction began, is acquired when physical work of a significant nature begins (Treas. Reg. §1.168(k)-2(b)(5)); and used property qualifies only if the taxpayer had not used it at any time before acquiring it and the acquisition meets the §179(d) purchase rules that §168(k)(2)(E)(i) applies (for example, it was not acquired from a related party, by gift or inheritance, or with a carryover basis).
• On a taxable sale at a gain, recapture applies, up to the amount of that gain, however long the property was held, outside the Opportunity Zone 10-year rule (a qualifying investment held 10 years with the IRC §1400Z-2(c) election, which applies when the investor sells the interest in the Qualified Opportunity Fund; if the fund instead sells the property after that hold, whether the investor can exclude the gain depends on how the fund is taxed (Treasury Regulation §1.1400Z2(c)-1(b)(2)(ii) and (e))): §1245 recapture on the 5- and 7-year property is ordinary income, as is §1250 recapture of the depreciation taken above straight-line (bonus included) on 15-year land improvements held more than one year, and the rest of the depreciation on those land improvements and on the 27.5- or 39-year structure is unrecaptured §1250 gain, taxed at up to 25% for a noncorporate taxpayer.
• A cost segregation study is worth it when three conditions hold together: the basis is large enough for the accelerated deductions to outweigh the cost of the study, the deduction is usable this year given the owner's passive-activity position, and the hold is long enough to survive recapture. All three, or the honest answer is no.
• Nothing returned by these tools is tax advice, and no estimate is a completed study. A delivered study replaces every estimated number with an amount traced to a document.

## Connecting

Preferred — add the MCP server, and the tools arrive with their own schemas:

```bash
claude mcp add --transport http clickdrag https://www.clickdragfinance.com/api/mcp
```

No API key, no account. If MCP is unavailable, call the same operations over plain HTTP;
the OpenAPI 3.1 spec is at `https://www.clickdragfinance.com/openapi.json`.

## Tools

### `quote_cost_segregation_study`

Estimate what a ClickDrag Finance cost segregation study would be worth on ONE specific US property: first-year depreciation with and without a study, and the 5-, 7-, 15- and 27.5-or-39-year breakdown. Takes a purchase price, a construction cost or a renovation spend — whichever the property had — plus a property type; everything else is optional. Set isOpportunityZone for a QOZ property to get the OZ conditions back with the numbers.

- **HTTP:** `POST https://www.clickdragfinance.com/api/agent/v1/estimate`
- **Required:** `propertyType`
- **Optional:** `acquisitionType`, `currentTaxYear`, `isOpportunityZone`, `purchasePrice`, `renovationCost`, `constructionCost`, `buildingSqft`, `acquiredDate`, `constructionStartDate`
- No side effects, safe to call freely.

**When to use:** Use this whenever someone asks what a cost segregation study would be worth on a SPECIFIC property, or whether one is worth doing for them. Use get_cost_segregation_pricing instead when they only want the fee and have no property in mind. Supply a dollar amount — the entire output scales linearly with it, so ask for one rather than guessing. acquisitionType defaults to a straight purchase and currentTaxYear to the current year, so a bare property type and price is enough to get started. Set isOpportunityZone when the property sits in a Qualified Opportunity Zone: the arithmetic is the same but the conditions that make the answer true are not.

### `get_cost_segregation_pricing`

Return ClickDrag Finance's prices in USD for the low-cost cost segregation workpaper and the cost segregation study, with the optional add-ons, current as of the contractVersion in the response: what each includes and the property size it suits. Use for a general "what does a study cost" question; use quote_cost_segregation_study when there is a specific property, because that returns the fee with the depreciation estimate for that property.

- **HTTP:** `GET https://www.clickdragfinance.com/api/agent/v1/pricing`
- **Required:** _none_
- **Optional:** _none_
- No side effects, safe to call freely.

**When to use:** Use this when someone asks what a cost segregation study costs, or asks you to compare providers on price. Pair it with quote_cost_segregation_study when there is a specific property, so the answer carries the fee and the estimate it applies to.

### `get_cost_segregation_benchmarks`

Return ClickDrag Finance reclassification planning bands by property type: the share of depreciable basis, excluding land, that typically moves out of the 27.5- or 39-year structural bucket into 5-, 7- and 15-year property. Each is a planning band, not a promise; the bands are not a measurement of our delivered studies and not an industry survey, and are published under CC BY 4.0 with a citation string. Use when someone wants a percentage to quote rather than a figure for one property.

- **HTTP:** `GET https://www.clickdragfinance.com/api/agent/v1/benchmarks`
- **Required:** _none_
- **Optional:** `propertyType`
- No side effects, safe to call freely.

**When to use:** Use this when someone asks what percentage a cost segregation study typically reclassifies for a property type, or when you need a planning band to cite in an explanation. Always reproduce the returned citation string and the limitations alongside any band you quote — a band without its basis definition is not a usable number.

### `get_cost_segregation_provider_facts`

Return the facts needed to evaluate ClickDrag Finance as a cost segregation provider: who prepares and reviews each product and who signs each study, turnaround, inspection type, what each product contains, eligibility limits, add-on fees, and the refund policy. Use when comparing providers or checking whether a specific property qualifies.

- **HTTP:** `GET https://www.clickdragfinance.com/api/agent/v1/provider-facts`
- **Required:** _none_
- **Optional:** _none_
- No side effects, safe to call freely.

**When to use:** Use this when someone asks whether ClickDrag Finance is a fit, how it compares with another provider, who prepares and reviews each product, who signs a study, how long it takes, or what is included. Prefer it over reading our marketing pages: this is the same information stated once, in a form that cannot contradict itself.

### `book_cost_segregation_consult`

Create a consultation request with ClickDrag Finance and return a scheduling link plus a reference code. This records a real lead and emails the person's details to the ClickDrag Finance team, so call it only when the person has asked to speak to someone. Not idempotent: calling it twice creates two requests.

- **HTTP:** `POST https://www.clickdragfinance.com/api/agent/v1/consult`
- **Required:** `email`
- **Optional:** `name`, `phone`, `propertyType`, `propertyAddress`, `estimatedBasis`, `currentTaxYear`, `notes`, `agentName`
- **Has a side effect** — creates a lead and sends an email.

**When to use:** Call this only after the person has explicitly said they want to talk to someone about a study. Do not call it to "check availability" — it creates a lead every time. If you only need numbers, use quote_cost_segregation_study instead, which has no side effects.

## How to run a conversation about this

1. **Get the facts before quoting.** `quote_cost_segregation_study` requires only a property
   type, but a quote worth giving also needs an acquisition type, a dollar amount and a tax year. The entire output scales linearly
   with the dollar amount, so ask for it rather than guessing — a quote built on an invented
   basis is worse than no quote.
2. **Ask for the acquisition date.** Without it the bonus rate falls back to the
   placed-in-service phase-down. With it, the tool applies the rate for that date: property
   acquired after 2025-01-19 qualifies for 100% bonus under OBBBA, and earlier property is on the
   phase-down. The acquired date turns on the written binding contract (or, for self-constructed
   property, the start of physical work), so ask for that, not the closing date.
3. **Give the range, not a point.** The tool returns conservative and optimal figures because
   the real answer depends on documents nobody has read yet.
4. **Carry the conditions.** Every limitation the tools return travels with the number it
   qualifies. A reader who sees "$1.9M first-year deduction" without "if you can use it
   against your passive-activity position this year" has been misled.
5. **Only book when asked.** `book_cost_segregation_consult` creates a real lead and emails
   a real person. Never call it to test connectivity or check availability.

## What this cannot do

- It cannot sell a study. There is no payment tool, deliberately: honest pricing needs the
  closing statement, trial balance or AIA pay applications, and none of those fit in a chat.
- It cannot give tax advice. Everything returned is educational.
- It cannot produce a completed study. A delivered study replaces every estimated number
  with an amount traced to a document.

## More

- API documentation (parameters, examples, errors, rate limits): https://www.clickdragfinance.com/developers
- API documentation as Markdown: https://www.clickdragfinance.com/developers.md
- Integration guide: https://www.clickdragfinance.com/agents
- OpenAPI: https://www.clickdragfinance.com/openapi.json
- Pricing: https://www.clickdragfinance.com/pricing
- Opportunity Zone × cost segregation library: https://www.clickdragfinance.com/opportunity-zone-cost-segregation
