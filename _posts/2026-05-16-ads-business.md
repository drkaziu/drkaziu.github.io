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

- Perfect callibration

![Perfect Callibration](/assets/images/perfect_callibration_graph.png)

- Overconfident model

![Overconfident Model](/assets/images/overconfident_callibration_graph.png)

- Callibration error

![Callibration Error](/assets/images/underconfident_callibration_graph.png)

- Systematically biased

![Systematically Biased](/assets/images/systematically_biased_graph.png)

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
  height="800"
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

![Placeholder](/assets/images/placeholder.png)
---

## Exploration vs Exploitation

The system must exploit known good ads while exploring uncertain ones to learn better long-term performance.

![Placeholder](/assets/images/placeholder.png)
---

## A/B Testing for Ads Systems

You must design experiments that detect impact on revenue, clicks, conversions, users, sellers, and long-term marketplace health.

![Placeholder](/assets/images/placeholder.png)

---

## Ads Diagnostics

When performance drops, you must identify whether the cause is ranking, targeting, auction dynamics, budget limits, supply-demand imbalance, tracking, or model drift.

![Placeholder](/assets/images/placeholder.png)

---
## Feedback Loops and Bias 

Ads systems learn from what they show, so bad ranking can create biased training data and reinforce itself.

![Placeholder](/assets/images/placeholder.png)

---
## Multi-Objective Constrained Optimization 

The hard part: optimize revenue, advertiser ROI, marketplace fairness, user engagement, privacy, latency, and business strategy at the same time.

![Placeholder](/assets/images/placeholder.png)



