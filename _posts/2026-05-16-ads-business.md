---
layout: post
title: "Ads Business 101"
date: 2026-05-16
tags: [ads, data, business]
---

![Ads intro](/assets/images/ads_intro.png)

## Ads Business Model

Ads generate revenue by selling attention, clicks, conversions, or promoted visibility while trying
not to damage user experience.

![Ads Business Model](/assets/images/ads_business_model.png)

The core tension in the ads model is captured in the feedback loop on the left:
the platform monetises user attention, but over-monetising degrades the experience,
which shrinks the attention pool, which shrinks revenue.
So there's a natural ceiling — not a moral one, just an economic one.

The four revenue types differ in what exactly is being sold and how risk is allocated:
- Impressions (CPM - cost per mille, where mille means 1000 impressions) — advertiser pays per view; platform bears zero performance risk.
- Clicks (CPC - cost per click) — advertiser pays only when someone acts; a bit more risk-sharing.
- Conversions (CPA - cost per action) — advertiser pays only on outcomes; platform takes on more risk, but prices are much higher.
- Promoted slots — fixed placement fees, independent of user behaviour; predictable for both sides.


---

## Ad Real Estate

The available places where ads can appear: feed slots, search results, item pages, category pages, notifications, etc.

![Ad Real Estate](/assets/images/ads_inventory_real_estate.png)

The diagram shows a schematic platform UI — think a marketplace or a social feed — with every ad-eligible surface marked in amber (paid) or purple (push), against the neutral gray of organic content.

A few things worth noticing in the layout:

The **search bar** is prime real estate — highest intent, so highest CPM. Whatever someone is actively searching for is exactly what advertisers want to intercept.

The **feed slot** sits next to organic items and is deliberately hard to distinguish at a glance — that proximity to organic content is intentional and is what makes it valuable.

The **banner** breaks the scroll and commands attention but interrupts the experience most aggressively — the classic UX tension made visible.

The **item page** placement is interesting because the user is already in buying mode, so conversion rates are high even though the audience is smaller.

**Push notifications** are a separate channel entirely — they reach users outside the platform, which is why they're marked in purple rather than amber.

---

## Ad Real Estate in Unconventional Spots

There can also be unconventional and unexpected placements for ads.

![Ad Real Estate Unconventional](/assets/images/ads_inventory_unconventional.png)

These surfaces are interesting precisely because they're unexpected. A few worth highlighting:

**Zero-results page** is arguably the most underrated slot. The user searched for something the platform can't supply — that's a user with specific intent and no organic result competing for their attention. A brand can step in perfectly.

**In-chat sponsored message** might be most distinctive surface. The chat thread between buyer and seller is where the transaction actually happens — injecting a shipping partner offer ("send with DPD for €2.49") feels like a service, not an intrusion, which is why it converts well.

**Listing creation flow** flips the model — instead of targeting buyers, it targets sellers at the moment they're most engaged with a specific category. A laundry brand appearing while someone lists a pile of clothes is contextually perfect.

**Post-purchase screen** is the highest-trust moment in any commerce app — the user just had a positive experience, their guard is down, and they're emotionally receptive. It's chronically undermonetised relative to its value.

**Loading/skeleton screens** exploit captive attention: there's nothing to scroll, nothing to tap, so the eye has nowhere else to go. Brief but highly visible.

---

## Advertiser objective

What the advertiser wants: impressions, clicks, purchases, app installs, brand awareness, or marketplace engagement.

![Advertiser Objectives](/assets/images/advertiser_objectives.png)

The funnel shape is the key structural idea here — advertiser objectives aren't equal, they map to different stages of a buyer's journey, and the audience gets smaller (and more valuable) as you go deeper.

A few things worth noting across the four stages:

**Awareness** is the most expensive in absolute terms but the hardest to measure. You're paying for eyeballs with no guarantee of action, which is why CPM dominates here. Brand advertisers — fashion labels, car makers, FMCG (fast-moving consumer goods - these are everyday products that sell quickly and are bought often) — live at this stage.

**Consideration** is where intent signals start appearing. Someone clicking an ad is raising their hand. CPC pricing shifts some risk to the platform — if nobody clicks, the advertiser pays nothing.

**Conversion** is where e-commerce advertisers concentrate most of their budget. CPA and ROAS (Return on ad spend) become the language — not "how many people saw this" but "how many euros came back for every euro spent." App install campaigns also live here; the install is the conversion event.

**Retention** is the most underrated stage. Acquiring a new customer costs 5–7× more than keeping an existing one, so re-engagement ads (push notifications, loyalty promos, email-triggered display) targeting people who already bought are extremely high-ROAS by comparison — but few platforms build proper inventory for it.

---

## User Experience Guardrails

Ads must not make the app feel spammy, irrelevant, slow, or unfair to organic sellers.

![UX Guardrails](/assets/images/ux_guardrails.png)

Four guardrails, each with its own failure mode sitting in the corner — the secondary nodes show what breaks when the guardrail is ignored.

A few things worth unpacking:

**Spamminess** is the most visible guardrail and the one platforms track most carefully. Frequency caps (how many times one user sees one ad) and slot ratios (e.g. no more than 1 ad per 4 organic items) are the main levers. Violating this triggers ad blindness — users stop seeing ads entirely, which is worse than showing fewer.

**Relevance** is both a UX guardrail and a revenue mechanism. An irrelevant ad wastes the slot and annoys the user; a relevant one feels like a useful suggestion. This is why platforms invest heavily in targeting infrastructure — better targeting makes ads feel less like ads.

**Performance** is the most technically concrete guardrail. Ad creatives (especially video, interactive, or retargeted) can add hundreds of kilobytes to a page load. On mobile, every 100ms of added latency measurably increases bounce rate. Platforms enforce file size limits and lazy-load ad assets to protect core app speed.

**Fairness to organic sellers** is the most politically sensitive guardrail — and the most specific to marketplace apps. If the top 8 search results are all sponsored, small sellers with no ad budget become invisible regardless of product quality. This erodes their trust in the platform, they list elsewhere, supply thins, and the whole marketplace degrades. The fix is structural: cap the number of sponsored slots per page and label them clearly so users can still choose to scroll past.

---

## Core Ads Metrics

Understand impressions, clicks, CTR, CVR, CPC, CPM, CPA, ROAS, revenue per mille, fill rate, and ad load. This is a rich set of 11 metrics — the best approach is two diagrams: one showing how the metrics are derived from the same raw events (so you see the relationships), then one showing which metrics belong to which perspective (supply side vs. demand side).

First, the derivation chain — everything flows from the same three raw events.

![Ads Metrics](/assets/images/ads_metrics_derivation.png)

The derivation structure is the key insight: every metric is just arithmetic on the same three raw counts — impressions, clicks, conversions. CTR and CVR are efficiency ratios between adjacent events. CPM/CPC/CPA tell you what the advertiser paid per event. RPM, fill rate, and ad load are the platform's own view of its supply health.

Now the second diagram — same metrics, but arranged by who cares about them and why.

![Ads Metrics Perspectives](/assets/images/ads_metrics_perspectives.png)

The perspective split is what makes the metrics make sense. A few things worth noting across both diagrams:

CTR and CVR form a chain: CTR tells you if the creative and targeting are working (did anyone care enough to click?), CVR tells you if the landing page and offer are working (did anyone care enough to buy?). Low CTR with high CVR means good offer, bad targeting. High CTR with low CVR means good targeting, bad offer.

CPM vs. CPC vs. CPA is really about risk allocation. CPM: platform takes no risk, advertiser pays regardless of outcome. CPC: risk shared — platform only earns if someone clicks. CPA: most of the risk shifts to the platform or ad network, so CPA prices are much higher per unit, compensating for that guarantee.

RPM vs. CPM is an important distinction people miss. CPM is what the advertiser agreed to pay per thousand impressions. RPM is what the platform actually received per thousand impressions — accounting for unsold inventory, discounts, and ad network cuts. RPM is almost always lower than CPM, and the gap between them is a measure of how efficiently the platform is monetising its supply.

Fill rate and ad load are the platform's two levers for supply health. Fill rate below 100% means some slots went unsold (wasted inventory). Ad load measures how much of the experience is ads — too high and UX degrades, too low and revenue is left on the table.

---

## Marketplace Relevance

An ad is not good just because it pays. It must be relevant to the user, context, category, intent, and marketplace behavior.

![Marketplace Relevance](/assets/images/marketplace_relevance.png)

Five signals feed one score, and that score is a gate — not a ranking. The ad either clears the relevance threshold and enters the auction, or it gets filtered before bidding even begins. A high bid from an irrelevant ad loses to a lower bid from a relevant one, which is the core design principle.

The five signals are worth distinguishing:

**User and context** (purple) answer *who is here and where are they right now*. User signals are slow-moving — they accumulate over sessions and reflect stable preferences. Context signals are fast — they describe this specific moment: someone on a search results page at 9pm on mobile behaves differently than the same person on a product page at noon on desktop.

**Category and intent** (teal) answer *what are they looking for*. Category is coarse-grained — does the ad's product type match what the user is browsing? Intent is fine-grained — what did their search query actually say, how recently, and how deeply did they engage with similar items? A search for "vintage denim jacket" carries far stronger intent than passively scrolling a feed.

**Marketplace behaviour** (amber) is the track record signal — and it's the most distinctive to marketplace apps. A seller with a history of disputes and returns gets their ads penalised even if the bid is high. The historical CTR of the specific ad creative is also fed back in: an ad that nobody clicks gets deprioritised because past performance predicts future performance. This is why new ads sometimes need a "warming up" period.

The two-outcome split at the top makes an important point: relevance filtering is not the same as auction ranking. Filtering happens first and is binary. Only ads that clear it enter the second stage, where price and predicted CTR are combined into an effective CPM that determines the final ranking. High payment is necessary but not sufficient — relevance is the entry fee.
