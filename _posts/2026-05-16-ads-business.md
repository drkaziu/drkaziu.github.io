---
layout: post
title: "Ads Business 101"
date: 2026-05-16
updated: 2026-05-19
tags: [ads, data, business]
---

Advertising systems sit at the intersection of machine learning, microeconomics, and product engineering — and if you can hold all three in your head at once, you will find that most of what looks like complexity is actually a small set of well-defined trade-offs, repeated at scale and at speed. This is my attempt to work through that complexity, built with AI as a thinking partner.

![Ads intro](/assets/images/ads_intro_v2.jpeg)

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

## Advertiser Objective

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

---

## Ranking

Deciding which ad or promoted item should appear first based on predicted value, relevance, bid, quality, and constraints.

![Ad Ranking Pipeline](/assets/images/ad_ranking_pipeline.png)

The pipeline has two exit points — both before the final slot is filled. Now the scoring formula itself deserves its own diagram, because the multiplication of three factors is the core idea most people miss.

![Ad Ranking Score](/assets/images/ad_ranking_score_anatomy.png)

The two diagrams tell a complete story. The pipeline shows the sequence of gates; the score anatomy shows why high payment alone is not enough.

A few things worth internalising:

The pipeline has two kill points, not one. Most people assume ranking is a single competition where the highest bidder wins. In reality, relevance filtering happens first — an irrelevant ad never enters the auction at all. Then after scoring, constraint application can suppress a top-scoring ad (e.g. it's already been shown to this user twice today, or it's in a category the platform has limited). Bid only matters in the middle stage.

The multiplication in eCPM is the key mechanic. If quality and relevance were added as bonuses — **bid + quality + CTR** — then a very high bid could always compensate for being irrelevant. Multiplication means that a near-zero predicted CTR collapses the whole score regardless of bid. This is intentional: it makes the system self-correcting. Ads that nobody clicks get penalised into irrelevance, which aligns advertiser and platform incentives around actual user response.

Ad B in the example wins with €2.00 vs Ad A's €4.00 because its relevance lifts predicted CTR from 0.5% to 3.2% — a 6.4× difference that no bid advantage can overcome. This is why marketplaces invest so heavily in targeting infrastructure: better targeting raises predicted CTR, which raises eCPM, which means the platform earns more even from the same bid pool.

Constraints at stage 4 protect things bid and quality cannot: frequency (don't annoy the same user), diversity (don't show five ads from one category in a row), and brand safety (don't place a children's toy ad next to a violent item listing). These are hard overrides — no score is high enough to bypass them.

---

## Targeting

Choosing which users or contexts should be eligible for an ad using signals like category interest, browsing behavior, location, device, and intent.

![Ad Targeting](/assets/images/ad_targeting.png)

Five signal types, one eligibility gate, four targeting modes in the bottom row. The colour split is meaningful — purple signals are about the user's history (slow-moving, accumulated across sessions), teal signals are about the current context (fast, specific to this moment), and amber is the live intent signal which is both the strongest and the most perishable.

A few distinctions worth unpacking:

Category interest vs intent is a temporal difference. Category interest says "this person has generally been interested in fashion over the past two weeks." Intent says "this person just typed 'linen summer dress' 40 seconds ago." Both are valuable, but they serve different campaign goals — interest drives brand awareness, intent drives conversion. The best campaigns layer both: the user must have shown category interest and have a live signal.

The eligibility engine combines rules with AND/OR logic. An advertiser might set: "target users in Lithuania AND who browsed footwear in the last 7 days AND on mobile." All three conditions must hold. Relaxing one to OR widens reach but reduces precision. Advertisers constantly tune this tradeoff — narrow targeting wastes fewer impressions but may not fill the budget; broad targeting fills budget but pays for clicks that don't convert.

The four targeting modes differ by what data they use. Broad match uses only platform-level category signals — no user-level data needed, which makes it privacy-safe but imprecise. Retargeting is the highest-intent mode: the user already visited the product or added it to a cart, so the ad is a reminder, not an introduction. Lookalike targeting finds users who statistically resemble past converters — it extends the reach of retargeting to cold audiences without requiring them to have visited before. Contextual targeting uses only the current page content and no personal history at all, which has become increasingly important as cookie tracking and mobile identifiers are being restricted.

Location and device are often underestimated as signals. Location determines not just geography but shipping feasibility — there is no point showing an ad for a seller who cannot ship to the user's country. Device shapes the creative format and the conversion path: mobile users convert differently from desktop users, and app users differently from browser users.

---

## Candidate Selection

Before ranking, the system must retrieve a smaller set of possible ads/items from a huge pool of eligible candidates.

![Ad Targeting](/assets/images/candidate_selection.png)

The funnel shape is the right mental model here — each stage is cheaper than the next, and the whole point is to make the expensive final stage as small as possible.

The key insight is in the bottom box: the full ranker is computationally heavy — it runs a complex model that evaluates bid, predicted CTR, quality score, and constraints simultaneously. Doing that for 10 million candidates on every page load, within 100ms, is physically impossible. Candidate selection is the engineering solution that makes ranking tractable.

Each stage has a different character:

Hard filters are deterministic and instant — pure database lookups. "Does this ad have an active budget? Does it target this user's country? Is it in the right category?" No ML involved, just boolean logic. This is where the bulk of candidates are eliminated cheaply.

Embedding retrieval is the most interesting stage. Both the user context and each ad are encoded as vectors in a shared semantic space. Finding the nearest neighbours to the user vector — ads that are semantically closest to what the user is looking at — can be done in milliseconds using approximate nearest neighbour (ANN) algorithms like FAISS or ScaNN. This is how the system finds relevant ads even when there's no exact keyword match: "linen trousers" can surface ads for "summer chinos" because they're close in embedding space.

The light scorer is a fast, shallow model — maybe a few decision tree layers or a tiny neural network — that runs on the ~10K survivors and prunes the bottom half quickly. It's a cheap approximation of the full ranker's judgment. The cost of running it on 10K items is trivial compared to running the full ranker on even 1K.

By the time the full ranker sees the candidate set, it's dealing with ~100–500 items — all of which are already known to be eligible, semantically relevant, and roughly worthwhile. The ranker can then apply its full cost, running a deep model that would have been unthinkable at 10M scale.

---

## Prediction Models

Models estimate probabilities such as *will this user click?*, *will this convert?*, or *will this ad harm engagement?*

![Prediction Models](/assets/images/prediction_models.png)

Three models, one decision — but the roles are distinct and the failure modes are completely different.

pCTR is the workhorse. It feeds directly into the eCPM formula (bid × pCTR), which means every ranking decision in the entire system runs through it thousands of times per second. The model is typically a deep neural network trained on logged user interactions — click or no-click — with hundreds of features spanning user history, ad creative, slot position, time of day, and query context. Position bias is a significant training challenge: ads shown in slot 1 get clicked more simply because they're in slot 1, which inflates their apparent CTR. Models must correct for this, usually by injecting position as a feature or using inverse propensity weighting.

pCVR is slower and sparser to train. Conversions happen far less frequently than clicks, so the signal is noisy — for niche categories, a new ad might have zero conversions in its first days of running. Platforms typically address this with Bayesian priors (assume a new ad converts at the category average until evidence accumulates), hierarchical models (borrow signal from similar ads), or cascaded models (predict pCVR given a click, then combine with pCTR to get the end-to-end expected conversion probability).

The harm model is structurally different — it is a veto rather than a weight. Where pCTR and pCVR contribute additively to expected value, a high harm score can suppress an ad entirely, regardless of its bid or predicted performance. What counts as "harm" varies: repeat exposure to the same user, low-quality creative that increases app abandonment, categories associated with high return rates, or formats that slow page load. Some platforms run multiple specialised harm models rather than one — a separate model for engagement harm, one for brand safety, one for seller quality.

The calibration point at the bottom is the subtlest and most important. A model that correctly ranks ads relative to each other but outputs systematically inflated or deflated probabilities will break the eCPM formula — because eCPM is used not just for ranking but for setting the actual price charged. If pCTR = 0.10 but only 2% of such impressions actually click, the platform overcharges advertisers and the whole pricing model becomes unstable. Calibration — ensuring that a predicted probability of 3% corresponds to a real-world frequency of ~3% — is maintained through regular recalibration passes using held-out data, temperature scaling, and isotonic regression.

---

## Calibration

Predicted probabilities must match reality; if a model says 15% click probability, roughly 15% should actually click. The graph perfectly illustrates the concept. The gap between the dot (what the model predicts) and the cross (what should happen in a perfect world) is calibration error made visible.

- **Perfect callibration:**

![Perfect Callibration](/assets/images/perfect_callibration_graph_v2.png)

- **Overconfident model:**

![Overconfident Model](/assets/images/overconfident_callibration_graph_v2.png)

- **Underconfident model:**

![Callibration Error](/assets/images/underconfident_callibration_graph_v2.png)

- **Systematically biased:**

![Systematically Biased](/assets/images/systematically_biased_graph_2.png)

Four failure modes, each with a different financial consequence:

A perfectly calibrated model's curve runs along the diagonal. pCTR = 5% means 5 in 100 impressions actually produce a click. The eCPM formula works as designed — bid × 0.05 × quality score produces a number that correctly reflects expected value, and advertisers are charged fairly.

An overconfident model's curve bends below the diagonal — it thinks clicks are more likely than they are. At high predicted probabilities, the actual rate is much lower. eCPM is inflated, so advertisers overpay for each slot. When they later measure campaign performance and see the true CTR, they conclude the platform is expensive relative to results, and they reduce spend or leave. The damage is slow but structural.

An underconfident model bends above the diagonal — it systematically under-predicts. eCPM is too low, good ads are ranked below their true value, the platform earns less than it should, and the ranking order is distorted. Budget is not allocated where it would do the most work.

A systematically biased model is the worst case: it might be miscalibrated in different directions at different probability levels — typically compressing the middle range (predicting 5–15% as 8–12%) or having a position bias baked in (slot 1 ads always predicted higher than they should be). This creates a ranking that's not just inaccurate but inconsistently inaccurate — impossible to correct uniformly.

The fix for all of these is the same process: after a model ships, collect a held-out set of impressions with known outcomes, plot the predicted vs actual curve, measure the gap (Expected Calibration Error, or ECE), then apply temperature scaling or isotonic regression to bend the curve back toward the diagonal. This recalibration pass runs regularly — often weekly — because model predictions drift as user behaviour changes.

---

## Objective Functions

You need to turn vague goals like “maximize good revenue” into mathematical logic balancing revenue, relevance, advertiser value, and UX.

<iframe
  src="/assets/interactive/objective_function_interactive.html"
  width="100%"
  height="890"
  style="border: 1px solid #ddd; border-radius: 12px;"
></iframe>

Try the four presets, then drag the sliders manually — the winner changes without any of the underlying ad data changing at all. That's the core insight: the objective function is the policy. Choosing weights is not a technical detail, it's a values decision disguised as arithmetic.

A few things the widget makes visible:

Revenue-first is a trap with a slow fuse. Ad A wins immediately, revenue looks good in the weekly report, but its low pCTR and poor UX score mean users gradually tune out — engagement drifts down, the CTR the model was trained on becomes stale, and in six months the pCTR predictions are broken. You've taught the system to prefer ads that users dislike.

UX-first undermonetises. Ad C has a beautiful experience score but a bid of 2. The platform leaves money on the table on every impression, which means fewer resources to improve the product, which eventually degrades the experience anyway. A marketplace that can't sustain its revenue can't maintain its supply either.

Seller-fairness mode is the most politically complex. It deliberately handicaps large advertisers to give smaller sellers visibility. This is a legitimate policy choice — it protects the diversity of the marketplace — but it comes at a cost to allocative efficiency. The advertiser willing to pay the most is not always the one who gets shown. Platforms make this tradeoff explicitly or implicitly, and it shapes the entire character of the marketplace.

The formula shown in the widget is a weighted linear combination — the simplest possible form. Real objective functions add non-linearities (logarithmic bid dampening to prevent pure pay-to-win), interaction terms (relevance × bid rather than just relevance + bid), and hard constraints that sit outside the objective entirely (a harm score above a threshold is a veto, not just a penalty). The linear version is useful for building intuition; the real version is messier and more defensible.

---

## Auctions and Bidding

Ads often compete through auctions where bid, predicted quality, and relevance determine winner and price.

![Auction Explainer](/assets/images/auction_explainer.png)

The quality score is the key mechanic to internalise. Ad A bids €12 but has quality 0.4, so its eCPM is €4.80. Ad B bids only €7 but has quality 0.9, giving eCPM €6.30. Ad B wins despite the lower bid. This is the same multiplication from ranking — quality isn't an additive bonus, it's a multiplier that can completely invert the bid order.

The three auction types differ in one dimension: what does the winner actually pay?

Second-price (Vickrey) is the theoretical ideal. The winner pays what the second-place bidder would have needed to win — not their own bid. This creates a dominant strategy: bid your true value, because the price you pay is set by someone else. There's no advantage to bidding low (you might lose) or high (you pay your own inflated bid in a first-price world, but not here). Honest bidding is the equilibrium, which means the auction efficiently allocates the slot to whoever values it most. Google's AdWords used this design from the beginning — it was one of the reasons the system scaled so cleanly.

First-price reverses the incentive. The winner pays exactly what they bid, so everyone shades their bids below true value to avoid the "winner's curse" of overpaying. The resulting game theory is messier — advertisers need to predict competitors' bids to set their own optimally, which creates an arms race of bidding algorithms. Many programmatic display exchanges switched from second-price to first-price around 2019, partly because publishers felt second-price was systematically underpricing their inventory.

Generalised second-price (GSP) extends the mechanism to multiple slots — a search results page might have three ad positions, each with different click-through rates. Each slot's winner pays the minimum they'd need to maintain their position: the eCPM of the bidder just below them, divided by their own quality score. GSP isn't theoretically equivalent to a repeated Vickrey auction (it can produce non-truthful equilibria), but it's simple enough to implement at scale and the incentive distortions are usually small in practice.

One important real-world detail: the "bid" an advertiser submits is almost never the price they pay. The actual clearing price is computed by the auction mechanism after all bids are in — and in most platforms it's further adjusted by bid floors (minimum acceptable prices), reserve prices (the platform's own implicit bid to not show any ad rather than a low-quality one), and occasionally price shading algorithms that adjust submitted bids downward before the auction runs.

In practical words:

The bar chart in section 1 makes the quality-multiplier effect immediately visible — Ad A's €12 bid shrinks to a shorter bar than Ad B's €7 bid, simply because 0.4 vs 0.9 is a bigger difference than €12 vs €7. That's the whole game.

Section 2 shows why second-price is the canonical design. Ad B wins with eCPM €6.30, but pays €6.00 — not €7.00 (its own bid) and not €6.30 (its own eCPM). The clearing price is derived from the runner-up: 2nd eCPM (€5.40) divided by the winner's quality (0.9). The winner captures the gap between what they were willing to pay and what the market required — that surplus is the advertiser's reward for having good quality.

Section 3 makes the price comparison concrete. Same bids, same winner, three different prices: €6.00 in second-price, €7.00 in first-price, and a cascade of prices in GSP depending on which slot. First-price's €7.00 price is why rational advertisers shade their bids downward there — they know they'll pay exactly what they bid, so they guess what competitors might bid and bid just above that. It's strategically complex and produces less efficient allocation than second-price.

---

## Pacing

Spending advertiser budgets smoothly over time instead of exhausting them too early or underdelivering.

![Pacing Explainer](/assets/images/pacing_explainer.png)

Three panels, one idea: spend should track a straight line from zero to budget across the day — anything that deviates from that line is a failure in one direction or another.

The throttle mechanism in the middle section is the core engineering. At any moment, the system computes a pacing ratio: actual spend divided by expected spend at this time of day. If expected spend at 09:00 is 37.5% of budget (9/24 hours elapsed) and the campaign has already spent 55%, the ratio is 1.47 — well ahead. The system responds by randomly skipping a fraction of eligible auction requests, proportional to how far ahead the campaign is. No bid is changed, no quality signal is altered — the campaign simply sits out some auctions it would otherwise have entered. When the ratio falls back toward 1, it re-enters full participation.

This random throttling matters because the alternative — stopping cold and restarting — creates visible gaps in coverage and disturbs the delivery patterns that downstream reporting relies on.

Front-loading is the most common failure mode and usually has a structural cause: high bids compete aggressively in the cheap early-morning auctions (when few other advertisers are bidding), burn through budget by mid-morning, and disappear exactly when user traffic peaks in the evening. The advertiser pays for a day's worth of impressions but gets a morning's worth of reach.

Underdelivery is the opposite problem and harder to diagnose because it can come from many places: targeting too narrow to find enough eligible auctions, bid floor too low to win any, creative rejected by quality filters, or simply a category with thin inventory. The platform fails to serve what was paid for, and the advertiser — who may not notice for days — loses trust in the system's reliability.

The practical challenge is that "the day" is not uniform. Auction volume is 10× higher at 20:00 than at 04:00. A purely time-proportional pacing target is naïve — spending 37.5% of budget by 09:00 means spending it during low-traffic hours, which is wasteful. Sophisticated pacing systems model historical traffic patterns by hour and day-of-week to produce a non-linear target curve, so the campaign enters prime-time auctions with budget still available to compete.

---

## Budget Allocation

Deciding where limited ad budget should go across users, markets, placements, campaigns, and time periods.

![Ads Budget Allocation](/assets/images/budget_allocation.png)

Five dimensions radiate from one fixed budget, and the core challenge is that they are not independent — a decision on one constrains all the others.

Each dimension has its own logic for how to split:

Campaigns are the highest-level split and the most strategic. The classic tension is between awareness (broad reach, hard to measure, long payback) and conversion (narrow targeting, easy to measure, short payback). Most advertisers over-invest in conversion campaigns because the attribution is clear, and systematically under-invest in awareness because the return is diffuse and delayed. Platforms encourage awareness spend partly for this reason — it's genuinely valuable but undersupplied.

Markets are split by opportunity size and historical efficiency. A market with high ROAS gets more budget; a new market gets a test allocation until it earns a larger share. The failure mode is over-concentration: pouring budget into one market because it has clear data while ignoring markets where the data is thin but the opportunity might be large.

Placements differ in cost, intent level, and conversion path. Search has the highest intent but limited inventory. Feed has scale but lower intent. Allocating across placements is essentially a portfolio problem — you want enough inventory in each to fill your budget, but you want to weight toward the placements with the best return for your specific objective.

User segments create the most interesting tension. Retargeting (previous visitors, abandoned carts) has very high conversion rates and low acquisition cost per conversion — but the audience is finite and saturates quickly. Prospecting (new users via lookalike or broad targeting) has lower conversion rates but is the only way to grow. Budget split here is directly a bet on growth rate vs short-term efficiency.

Time periods interact with pacing but operate at a different level — pacing distributes spend within a day, whereas time allocation decides which days or hours get more budget. Dayparting (concentrating spend in peak hours) can dramatically improve ROAS for some categories — a food delivery app should weight evenings heavily; a B2B SaaS should weight weekday business hours.

The three methods at the bottom represent the maturity curve of how advertisers manage this complexity. Rule-based allocation is where everyone starts — 40% to conversion, 30% to awareness, 20% to retargeting, 10% to new markets. It's predictable and auditable but rigid. Optimised allocation uses performance signals to continuously shift budget toward whatever is producing the best return — effective but can collapse into a single segment if not constrained. Portfolio management is the most sophisticated approach: campaigns share a pool and a central optimizer reallocates daily or even hourly, subject to minimum spend floors per segment to prevent complete neglect of long-term goals.

---

## Exploration vs Exploitation

The system must exploit known good ads while exploring uncertain ones to learn better long-term performance.

![Explore vs Exploit in Ads](/assets/images/explore_exploit.png)

The regret chart is the key visual. Regret is the cumulative cost of not always showing the best possible ad — the gap between what you earned and what you could have earned with perfect information. All three strategies accumulate regret, but their curves diverge:

Pure exploitation accumulates regret slowly at first, because it confidently shows known-good ads. But it misses the fact that some untested ads might be even better, and that gap compounds permanently. The curve never flattens — it keeps climbing at a steady rate because the system never discovers what it's missing.

Pure exploration accumulates regret quickly — you're constantly showing uncertain ads, many of which are bad, and paying the cost in wasted impressions. The curve eventually slows as every ad becomes well-understood, but by then enormous budget has been burned on bad placements.

A balanced strategy (UCB or Thompson sampling) pays slightly more regret early — it does explore, and some of that exploration is costly — but the curve bends and flattens over time as it learns which ads are genuinely good and stops wasting budget on the confirmed bad ones. The long-run regret is sublinear, meaning the cost of uncertainty shrinks relative to total traffic.

The cold-start problem in the bottom box is worth dwelling on. A new ad enters the system with zero impressions and zero clicks — its predicted CTR is undefined, so the pCTR model falls back to a category prior (e.g. "fashion ads average 2%"). That prior gets it a few impressions. If those impressions produce no clicks, the model updates downward and the ad sinks in ranking. But maybe it was just bad luck — 10 impressions is a tiny sample. Without a deliberate exploration mechanism, the ad may never accumulate enough data to be evaluated fairly. This is why platforms often give new ads an "exploration budget" — a guaranteed floor of impressions regardless of predicted CTR — specifically to break this cycle.

The three strategies differ in sophistication. Epsilon-greedy is the easiest to implement and explain to advertisers ("10% of your traffic is used for testing"). UCB adds an explicit uncertainty bonus to each ad's score: ads with fewer impressions get a boost proportional to how uncertain their estimated CTR is, so the system naturally gravitates toward testing the most uncertain candidates first. Thompson sampling goes further — it maintains a probability distribution over each ad's true CTR, samples from it at decision time, and shows whichever ad's sample is highest. This naturally concentrates exploration on ads where the distribution is wide (uncertain) and exploitation on ads where it is narrow (well-understood), without any manually tuned ε parameter.

---

## A/B Testing for Ads Systems

You must design experiments that detect impact on revenue, clicks, conversions, users, sellers, and long-term marketplace health.

![Ads AB Test](/assets/images/ab_testing_ads.png)

Ad system experiments are structurally harder than product experiments because the outcomes are entangled across four different stakeholders simultaneously — and each stakeholder's signals move at a different speed.

The metric layer stack is the central idea. You cannot reduce an ad experiment to a single primary metric. A change that raises RPM but increases ad complaints is not straightforwardly good — you've found short-term revenue by damaging long-term engagement. A change that improves CTR but buries organic seller listings shifts value from sellers to advertisers in a way that may erode marketplace supply over months. Every experiment needs to be read across all five layers before a decision is made, and the layers must be read in order of time horizon: revenue moves in hours, marketplace health moves in weeks.

The three validity threats are specific to marketplace ad experiments and don't appear in standard product A/B testing:

Network interference is the most technically difficult. In a two-sided marketplace, the control and treatment groups share the same inventory pool. If the treatment group generates more impressions at lower CPM (because relevance improved and competition increased), advertisers in the control group see their bids go further — they get more for the same spend. The control group is contaminated, and the measured lift is understated. The standard fix is to randomise at the market or seller level rather than the user level — geo-based holdouts, where one city sees the control and another sees the treatment, break the interference at the cost of reduced statistical power.

Novelty effect is familiar from product experiments but hits ad formats especially hard. A new ad unit design gets extra clicks simply because it's new — users notice it, curiosity drives clicks, and the CTR looks excellent. Run the same format for four weeks and the effect fades as users habituate. Experiments need to run long enough (typically two to four weeks) that novelty wears off before you read the result.

Budget reallocation bias is subtler. Sophisticated advertisers monitor campaign performance in near-real-time. If their ads in the treatment bucket are performing better, they shift budget toward that campaign — which increases auction competition in the treatment, raising prices and changing the dynamics the experiment was designed to measure. The group assignment is still random, but the bids are no longer comparable.

The three decision outcomes in the bottom row reflect the reality that "statistically significant" is not sufficient for a ship decision. A result can be significant and still wrong — significant revenue lift with significant user harm is a hold, not a ship. The bar for killing is lower than the bar for shipping: evidence of harm is acted on faster than evidence of benefit, which is the correct asymmetry for a system users depend on.

---

## Ads Diagnostics

When performance drops, you must identify whether the cause is ranking, targeting, auction dynamics, budget limits, supply-demand imbalance, tracking, or model drift.

![Ads Diagnostics](/assets/images/ads_diagnostics.png)

The triage order at the bottom is the most practically useful thing in the diagram. Every experienced ads engineer learns this the hard way: before you touch a model, recheck targeting logic, or raise bids — rule out tracking failure first. A broken pixel or a lost conversion tag looks identical to every other performance drop in your dashboard metrics. Conversions cliff, ROAS collapses, the on-call engineer starts blaming the ranking model — but the system is working perfectly and nobody is measuring it correctly. This happens after iOS privacy updates, after tag manager deploys, after third-party SDK upgrades. Always check event logs and pixel firing before anything else.

Budget exhaustion comes next because it's equally fast to diagnose and equally deceptive. Delivery cliffing — impressions going to zero at a specific time of day — is the giveaway. If you see this pattern, look at pacing logs before you look at anything else.

Auction dynamics are trickier because they're external. A drop in win rate with a simultaneous rise in clearing price means competitors have entered your inventory. The fix is not a model change — it's a bid adjustment or quality score improvement. Mistaking a competitive shift for a ranking failure and rolling back a model is a classic error.

Ranking and targeting failures are often confused with each other. The distinguishing signal is where in the pipeline the numbers shrink. If candidate volume (the output of retrieval) is normal but eCPM scores are suddenly lower, the ranking model has a problem — a feature pipeline failure, a bad model deployment, a training data issue. If candidate volume itself shrank, the targeting or retrieval system is the problem — a user feature lookup failing silently, a segment definition that's now returning empty, an embedding index that hasn't been refreshed.

Model drift is the slowest and most insidious. It doesn't cliff — it degrades over weeks. The signal is calibration: pCTR predictions that used to match observed CTR start diverging, slowly and then faster. Seasonal behaviour shifts (summer vs. winter buying patterns), platform changes (a new ad format that the model wasn't trained on), or changes in user demographics all cause drift without any code change. The only durable fix is continuous retraining on recent data combined with automated calibration monitoring that fires an alert when the predicted-vs-actual gap exceeds a threshold.

---

## Feedback Loops and Bias 

Ads systems learn from what they show, so bad ranking can create biased training data and reinforce itself.

![Ads Bias Feedback Loops](/assets/images/feedback_loops_bias.png)

The red cycle at the top is the core mechanism. Once an ad wins slot 1, it accumulates clicks — not because it's necessarily the best ad, but because slot 1 always gets more attention. Those clicks go into the training log. The model retrains on that log and learns that this ad is high-quality. It ranks the ad first again. The cycle locks in, and the feedback loop does the rest.

This is not a bug in one system — it's a structural property of any system that learns from its own outputs. Every recommendation system, search engine, and content feed faces the same dynamic. The difference in ad systems is that money flows through the rankings, so the consequences are financial and the biases are commercially exploitable.

The three bias types are distinct problems that compound each other:

Position bias is the most quantified. Slot 1 in a typical feed or search result receives roughly 8–10× the clicks of slot 5, holding ad quality constant. This has been measured through randomised position experiments where the same ad is randomly assigned different slots. The effect is so large that a mediocre ad in slot 1 will appear to outperform an excellent ad in slot 4 in any naive CTR comparison.

Exposure bias is the invisible half. An ad that never gets shown has no click signal at all — the model treats this as evidence that it has low CTR, when actually it has no information. The model penalises uncertainty the same way it penalises poor performance, which means new and unlucky ads spiral downward not because they're bad but because they haven't had the chance to prove themselves.

Selection bias is the meta-problem: the training data is not a random sample of ad-user-context combinations. It's a highly non-random sample of exactly the combinations the current model preferred. You cannot train your way out of this without changing what you show.

The three debiasing techniques address the problem from different angles. Inverse propensity scoring (IPS) is a statistical correction applied during training — each click is reweighted by the inverse of the probability that the ad was shown in that position. A slot-1 click is downweighted because it was very likely to happen regardless of ad quality; a slot-5 click is upweighted because it's a stronger signal. This corrects for position bias without changing what the system shows, but requires accurate propensity estimates.

Forced exploration directly generates counterfactual data by randomly promoting low-ranked ads into high positions on a small fraction of traffic. This is expensive (short-term revenue loss) but produces unbiased training signal. It's the only way to discover whether a currently low-ranked ad might actually be very good.

Counterfactual machine learning attempts to estimate what would have happened to an ad in positions it was never shown, using causal modelling and logged behaviour. It's the most technically ambitious approach and the most actively researched — but requires careful model assumptions to avoid simply learning a different kind of bias.

The bottom box is the philosophical root: you are epistemically blind to the outcomes you didn't cause. Every click you observe is a consequence of a decision you already made. The only way out is to make some decisions randomly, accept the short-term cost, and use that randomness to see the counterfactual world your model is hiding from you.

---

## Multi-Objective Constrained Optimization 

The hard part: optimize revenue, advertiser ROI, marketplace fairness, user engagement, privacy, latency, and business strategy at the same time.

Two diagrams: first the structure of the problem (what objectives conflict with what), then how the system actually resolves it in practice.

The tension map comes first — the objectives don't all pull in the same direction, and understanding which pairs conflict is the foundation of everything else.

![Ads Tension Model Map](/assets/images/moco_tension_map.png)

The tension map makes the hardness of the problem visible. Revenue and fairness are in strong conflict — the most efficient revenue extraction concentrates ads on high-bidding advertisers, which crowds out small sellers. Advertiser ROI and privacy are in strong conflict — the richer the user profile, the better the targeting, but privacy regulation deliberately degrades that profile. These aren't solvable tensions; they're permanent trade-offs that the system must navigate on every auction call.

Now the resolution structure — how does an actual system handle seven conflicting objectives at once?

![Ads Tension Model Map Extended](/assets/images/moco_resolution_structure.png)

The resolution structure is the practical answer to a theoretically intractable problem. You cannot simultaneously maximise seven conflicting objectives, so real systems decompose the problem into three ordered layers.

**Layer 1** converts some objectives into hard constraints — binary gates rather than continuous trade-offs. Latency is the clearest example: an ad that misses the 100ms serving deadline simply doesn't run, regardless of how good its eCPM is. The deadline is not a weight in a formula; it's a veto. Privacy floors work the same way: if a user hasn't consented to tracking, their ad targeting is degraded whether the system would prefer it or not. By converting objectives into constraints, you remove them from the optimisation problem and make the remaining problem tractable. This is also a governance mechanism — constraints are harder to override than weights.

**Layer 2** is the weighted objective function from earlier in this series — the place where policy is expressed as arithmetic. The critical insight on the diagram is that weights are value judgements, not technical parameters. Deciding that fairness should have weight 3 and revenue weight 5 is a product decision that encodes what the company believes a marketplace should do. When a regulator asks "why does your system favour large advertisers?", the honest answer lives in these weights.

**Layer 3** — the latency budget — shapes which models can be used at all. A deep neural network that would produce better relevance predictions than a gradient-boosted tree is irrelevant if it adds 80ms of inference time. This creates a continuous engineering pressure: any improvement in model quality that doesn't also fit the latency budget cannot ship. The cascade architecture is the practical resolution: use a fast, cheap model to score the full candidate set, then reserve the expensive model for the top 50 candidates where it matters most.

The Pareto frontier at the bottom is the conceptual foundation. For two objectives — say revenue and UX — the set of configurations where you cannot improve one without worsening the other forms a curve. Every point on that curve is "optimal" in the sense that nothing is being wasted. The choice of where on the curve to operate is a values decision. Moving off the frontier means you've found an improvement — you can get more of both — and that's engineering. Moving along the frontier is politics.


---

### Afterword

The engineer who understands why calibration matters, what the weights in an objective function actually say about a company's values, and where a performance drop is most likely hiding — that person is not just useful in an ads team; they are the person the team calls when the dashboard turns red at 11pm on a Friday, which is, as it turns out, the most reliable measure of whether you genuinely understand the system or merely know the vocabulary.



