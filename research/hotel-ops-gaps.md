# Harper Boutique Hotel — The WhatsApp Line as a Commercial and Operational Asset

**Scope:** operations, revenue and compliance. Not a product teardown, not a platform capability audit — two sibling documents cover those. Where a platform constraint or a competitor feature is load-bearing for a commercial argument it gets one sentence and no more.

**Property:** Harper Boutique Hotel, Sutera Avenue, Kota Kinabalu, Sabah. 9 room types, no on-site restaurant, reception on the 4th floor of a multi-block commercial development, front desk 07:00–22:00. Mixed domestic/regional/foreign guests, heavy OTA mix. Noise is the top complaint across ~288 reviews.

**Date of research:** 16 October 2026. Everything inferred rather than sourced is marked `(inf.)`.

> **Research limitation to note before relying on this.** The shared web-search budget for this session was exhausted before two verification queries could run: (a) the full text of the Personal Data Protection (Class of Data Users) Order 2013 as amended, and (b) the statutory definition of biometric data in s.4 PDPA as amended. Both points below rest on the DLA Piper *Data Protection Laws of the World* Malaysia chapter (last modified 12 Feb 2026) rather than the gazetted instrument. They are flagged in §4. Everything else is sourced as cited.

---

## 0. Baseline I am costing against

Harper does not publish its room count or rate. OTA listings disagree (38 rooms on tiket.com and Trip.com, "45 cozy rooms" on Hostelworld), and rate snapshots range RM147–US$38. The model below is therefore a sizing exercise, not Harper's P&L. Every line is `(inf.)` unless sourced.

| Input | Value | Basis |
|---|---|---|
| Rooms | 40 | Midpoint of 38–45 from OTA listings `(inf.)` |
| Room types | 9 | Given in brief |
| Occupancy | 58.5% | Kota Kinabalu AOR, Jan–Sep 2025 (Tourism Malaysia) — 2024: 55.0% |
| ADR | RM160 | OTA snapshot ~RM147 for a 2.5-star; rounded up `(inf.)` |
| Occupied room-nights/yr | 8,541 | 40 × 365 × 0.585 `(inf.)` |
| Room revenue/yr | ~RM1.37m | 8,541 × RM160 `(inf.)` |
| Average length of stay | 2.5 nights | `(inf.)` |
| Stays (arrivals)/yr | ~3,420 | 8,541 ÷ 2.5 `(inf.)` |
| OTA share of room-nights | 60% | "a lot of OTA bookers" in brief `(inf.)` |
| Foreign-guest share | ~36% | National hotel-guest split Jan–Sep 2025 is 64% domestic / 36% international (Tourism Malaysia); Harper's own split unknown `(inf.)` |

**Sanity check on scale, because it governs every recommendation below.** ~3,420 arrivals a year is about 9 a day. Harper is not a data-rich business. It cannot A/B test a 2-percentage-point effect, it will not accumulate 20,000 data subjects quickly, and it cannot support a tool that needs a full-time operator. Several of the "best practices" in the vendor literature are built for properties with 10–50× this volume and are actively wrong here. I flag those in §6.

**Two context figures that do transfer.** Sabah's average room rate for Jan–Sep 2025 was RM344.70, against a national RM238.40 — but that state figure is pulled up by the island and beach resorts, and a 2.5-star boutique in a city commercial block is nowhere near it `(inf.)`. And Malaysia's internet penetration was 97.7% at the start of 2025 with 34.9m users online; WhatsApp reach among internet users is credibly ~90% but rests on a single secondary source. The channel choice is not in question. What the channel *does* is.

---

## 1. The guest lifecycle a hotel line should cover

### 1.1 The stage-by-stage table

| Stage | What a good property does over messaging | What it earns or prevents | Harper today |
|---|---|---|---|
| **Enquiry** | Answers availability and rate questions in the guest's language; states a price with tax; sends a photo or a room-type comparison; captures the enquiry even when it does not convert | Converts the enquirer who would otherwise bounce to an OTA. Commission avoided on the margin | **Partial.** Answers in Malay/English/Chinese from 43 replies. Never states a price. Every rate and availability question is deflected to the website. No enquiry record, so no lost-enquiry count |
| **Booking** | Quotes, holds, takes a deposit or a card, confirms, sends the confirmation and the cancellation terms in-thread | Captures the booking in the channel where the conversation already is. Removes the website drop-off | **Partial, non-converting.** The bot routes to the website; a human takes over for anything commercial. A booking may happen, but it is not attributable to the line and not assisted by it |
| **Pre-arrival** | Initiates 24–72h out: confirms arrival time, states how to find the place, collects ID and tax-exemption proof, offers early check-in / upgrade / transfer, reconfirms | Arrival-day failures prevented; ancillary revenue earned; no-shows reduced; tax collected cleanly | **Absent.** No approved templates, so the hotel cannot speak first. No booking feed, so there is no event to speak about |
| **Arrival day** | Tells the guest the room is ready; re-sends directions; handles the late arrival explicitly; names the person on the desk | Prevents the lost-guest and locked-out-guest incidents that produce one-star reviews | **Reactive only.** A guest who messages gets an answer. The hotel cannot message first, and the bot is not time-aware — a 23:00 arrival gets the same reply as a 13:00 one, into a closed building |
| **In-stay** | Takes requests, routes them to a named person, closes the loop with the guest, escalates complaints, and catches the complaint *before* it becomes a review | Review-score protection; the complaint resolved in-house rather than in public; incremental sales (extensions, upgrades, laundry) | **Present, weakest link is fulfilment.** Requests become a storage row plus a 1:1 alert to a staff phone. No assignment, no acknowledgement, no timer, no completion, no confirmation back to the guest |
| **Departure** | Offers and prices late check-out on the morning; sends the folio; asks about lost property; confirms the deposit refund | Highest-margin ancillary sale in the hotel; disputes prevented | **Request intake only.** Late check-out exists as a staff request type, so a human can say yes. The hotel never offers it, never prices it, never confirms it in-thread, and never settles it |
| **Post-stay** | Thanks, asks for a review (or routes a low score privately first), returns lost property, sends a receipt | Review volume, which drives OTA ranking and occupancy; the private complaint instead of the public one | **Absent.** Nothing happens after check-out. No check-out event, no outbound capability |
| **Next stay** | Remembers the guest, remembers the preference, offers a direct rate to someone who came via an OTA last time, wins back the lapsed guest | The only genuinely zero-commission booking a hotel ever gets | **Absent.** No guest record across stays, no consent capture, no marketing template, no segmentation |

### 1.2 The three absent stages, argued

Wilfred expects three. There are three, and they are **pre-arrival, post-stay and next stay**. But the interesting part is not the count — it is that they are *one* failure wearing three costumes, and that they are precisely the stages where the money lives.

**The test I am applying.** "Absent" means no mechanism exists at all, not even a degraded one. A stage where the guest gets a worse answer than they should is *crippled*, not absent. A stage where nothing can happen under any circumstance is absent. That distinction matters because crippled stages are tuning problems and absent stages are capability problems, and they take different kinds of work.

**Pre-arrival is absent, doubly.** Two independent things are missing and either alone would be fatal. First, there are no approved message templates, so the hotel has no mechanism to open a conversation — WhatsApp will not deliver an un-templated business-initiated message outside an open customer-service window, and a guest who booked on Agoda three weeks ago has no open window. Second, even with templates there is no booking or arrival feed: no PMS, no booking-engine integration, no OTA reservation delivery into the line. So there is no event to trigger on and no list of who is arriving tomorrow. Harper could not send a pre-arrival message today even if it wanted to, and could not decide who to send it to even if it could send. That is absence, not degradation.

**Post-stay is absent for the same two reasons plus a third.** No check-out event exists in the line's world, no outbound mechanism exists, and there is no review-platform connection to close the loop against. The hotel cannot know a stay ended, cannot say anything if it did know, and cannot tell whether saying something worked.

**Next stay is absent for four reasons, which makes it the deepest hole.** There is no identity resolution across stays (a returning guest is a new phone number with no history, or the same phone number with no linked stay record). There is no PDPA consent capture, so even a perfect list could not lawfully be marketed to. There is no marketing template. And there is no segmentation — no way to distinguish "stayed twice, came via Agoda both times" from "enquired once, never booked", which is the only distinction that matters commercially.

**Why booking is crippled, not absent.** The line does participate: a guest asks about a room, gets an answer in their language, and gets pointed at the booking page. A human takes over for the commercial part. A booking can and does result. What is missing is the *close* — the price, the hold, the payment — and attribution. That is a real and expensive gap, addressed in §2, but it is a different kind of gap. Something happens; the wrong thing happens.

**Why arrival day is crippled, not absent — and why that is cold comfort.** The 43 canned replies almost certainly cover "where is reception", "what time is check-in", "how do I get there from the airport". A guest who messages at 14:00 is served. So a mechanism exists. But arrival day at *this* property is where partial presence does the most damage, and it deserves naming as the most dangerous stage rather than an absent one:

- Reception is on the **4th floor of a multi-block commercial development**. This is not a hotel with a lobby you walk into. A first-time guest with a suitcase has to find the right block, the right lift lobby, and the right floor.
- The desk closes at **22:00**. Kota Kinabalu International is 8km away and takes inbound flights late.
- The line **cannot message first**, so it cannot warn anyone about either fact before they are standing outside.
- The bot is **not time-aware** `(inf. — inferred from "43 ready-made replies" with no stated scheduling behaviour)`, so a 23:30 "I can't get in" produces a canned reply and a staff alert into a phone whose owner went home at 22:00.

So arrival day is present in the sense that a mechanism exists, and absent in the sense that the thing the guest actually needs — someone who knows they are coming, and someone awake when they arrive — does not. I rank it crippled on the mechanism test but treat it as a tier-one priority in §6 regardless, because the mechanism test is a description of the system, not of the guest's experience.

**Departure is the closest contender for a fourth.** It is worth being explicit about why it is not on the list. Late check-out exists as a staff request type, which means a guest who thinks to ask can get a yes. A mechanism exists, and it occasionally works. What is missing is offer, price, confirmation and settlement — all four of which are the *same* missing capability as everywhere else (initiate, and state a number). If someone wanted to argue departure as a fourth absent stage I would not fight hard; the honest position is that departure is the most crippled of the crippled stages, and that fixing pre-arrival fixes most of it as a side-effect, because the pre-arrival message is where you ask the departure question.

### 1.3 The structural reading — one gap, not three

The three absent stages are not three feature requests. They share exactly two root causes:

1. **The hotel cannot speak first** (no approved templates).
2. **The hotel does not know what is happening** (no booking, arrival, stay or check-out event feed).

Pre-arrival needs both. Post-stay needs both. Next stay needs both plus consent and identity. Every other stage is served, however badly, because in every other stage *the guest speaks first* and a canned reply is at least a reply.

This reframing is the most useful thing in this document, because it changes the shape of the work. It is not "build three lifecycle modules". It is "acquire the ability to initiate, and acquire a daily list of who is arriving and who left" — and the three stages then become template content, which is cheap. A manually pasted arrivals list and three approved templates buys most of three absent stages. A PMS integration buys the same thing with a six-month tail.

And the commercial consequence of the current shape is the headline finding of this whole document:

> **Harper's line operates only in the stages that cost money, and is absent from every stage that makes money.** In-stay service is a cost centre — necessary, review-protecting, but it does not ring a till. Pre-arrival, post-stay and next-stay are where ancillary revenue, review volume and zero-commission repeat business come from. The line has been built as a help desk and is being asked to justify itself as a commercial channel.

---

## 2. The money

### 2.1 Direct-booking deflection from OTA commission

**What Malaysian hotels actually pay.** The Malaysia Competition Commission's market review of the digital economy ecosystem under the Competition Act 2010 — Book 4, online travel agencies — is the only Malaysian-specific source worth quoting here. Its findings, as summarised by Richard Wee Chambers:

| Hotel type | Commission range | Source |
|---|---|---|
| Large chains | 10–18% | MyCC market review (OTA), via Richard Wee Chambers |
| Smaller hotels | 17–20% | Same |

Rates vary by booking volume and location. MyCC also found the sub-sector highly concentrated, with **Agoda and Booking.com each estimated at 30–40% market share in property bookings** in Malaysia. **Harper sits in the 17–20% band.** I will use 18%.

Two Malaysian specifics that the European literature does not give you:

- **Service Tax on Digital Services can sit on top of the platform fee**, so the effective cost is above the headline commission. Malaysia's SToDS collections rose to RM1.62bn in 2024 from RM802m in 2021, which indicates how comprehensively platform fees are now inside the tax net.
- **MyCC has flagged price parity clauses for investigation** and the Domestic Trade Minister, Armizan Mohd Ali, stated on 10 February 2026 that such clauses "restrict hotels from offering preferential rates through other platforms", forcing acceptance of high commission fees. The review carries 18 recommendations and was to go to Cabinet. **This is live, not settled.** For contrast, the position in Europe has already moved: the CJEU held in Case C-264/23 that neither wide nor narrow parity clauses qualify as ancillary restraints, and Booking.com removed or waived parity for EEA inventory under its DMA compliance report. Malaysia has not got there.

**What this means for a WhatsApp rate, practically.** Under narrow parity Harper would be barred from undercutting the OTA on its own public website. A quoted rate inside a one-to-one WhatsApp conversation is conventionally treated as a closed-user-group rate rather than a public rate, which is the standard route independents use to discount without breaching parity — but **this is a question about Harper's actual signed Agoda and Booking.com agreements, not a legal conclusion I can give** `(inf.)`. Note also that OTAs enforce by ranking demotion and loss of preferred-partner status even absent an enforceable clause, which for a property at 30–40%-share platforms is a real cost.

**A realistic shift.** The vendor literature offers large numbers. Cloudbeds is cited as finding independents gave 63.4% of bookings to OTAs in 2025 at an effective 18–30% per stay versus 5–12% direct; one agency reports a 9% median all-in cost per direct booking against 18–22% commission; Kalibri Labs is cited across ~18,000 US hotels for direct bookings being ~12.5% more profitable even after ad spend, and OTA business requiring up to 6.5× the acquisition investment. **All of those are US or European, mostly vendor-published, and none is a messaging-channel study.** They tell you direct is cheaper. They do not tell you a WhatsApp line will shift mix.

Here is the honest mechanism. A WhatsApp line does **not** win a first-time Agoda shopper away from Agoda — that guest never sees Harper's number until after they book. What it can convert is four much smaller pools:

1. The direct enquirer who messages and would otherwise bounce to an OTA.
2. The repeat guest who came via an OTA once and now has Harper's number.
3. The extension (§2.5) — which is a direct booking by definition.
4. The walk-in or last-minute local.

Modelled at 5 percentage points of mix shift over 12 months, which I regard as the top of the credible band for a property this size `(inf.)`:

| Line | Value |
|---|---|
| OTA-sourced room-nights at 60% mix | 5,125 |
| OTA-sourced revenue | ~RM820,000 |
| Commission at 18% | ~RM147,600/yr |
| Room-nights moved by a 5-point shift (60%→55%) | 427 |
| Revenue moved | ~RM68,300 |
| Commission avoided | ~RM12,300 |
| Less direct acquisition cost at 5–9% | RM3,400–6,100 |
| **Net annual benefit** | **~RM6,200–8,900** |

**That is the finding, and it is not the one people expect.** Commission deflection is the argument everyone leads with and it is worth under RM9,000 a year at Harper's scale. It is real, it compounds, and it is not where this line pays for itself.

### 2.2 Paid early check-in and late check-out

Harper's published times are check-in 15:00, check-out 12:00 (Hostelworld). That is a **three-hour turn window** — tight for housekeeping, which both limits how much late check-out you can sell on a full night and means the inventory you are selling is genuinely scarce. Good news for pricing, bad news for volume.

**Published conversion benchmarks, with provenance flagged.** These are the figures people will quote at you. Treat them with the stated caution:

| Benchmark | Figure | Source and caveat |
|---|---|---|
| Pre-arrival offers via guest messaging | 8–15% | Stayntouch (PMS vendor), unattributed |
| Pre-arrival digital upsells | 12–22% vs 3–7% at front desk | Stayntouch — **internally inconsistent**, the same article elsewhere gives front-desk at 15–20% and pre-arrival email at 2–5% |
| Late check-out offered on check-out morning | 18–28% at €25–€50 | Stayntouch, unattributed |
| Monetised early check-in / late check-out | 15–30% | Stayntouch, unattributed |
| Oaky pre-stay offers | ~13% conversion, 13.8× ROI | Vendor claim, undated |
| ROOMDEX client case | ECI/LCO = 68% of upsells; avg ECI US$35, LCO US$37; +28% to nightly rate | **One hotel, 30 days, vendor case study, base rate US$125** |
| Operator year of upsell data | ECI/LCO = 90% of upsell revenue, 96% of sales | Unattributed in source |
| Late check-out margin | 95–100% | Vendor estimate, unverified |

**Which of those transfer to Harper and which do not.** The *conversion rates* plausibly transfer — willingness to pay for a few more hours is not very culture-specific. The **prices do not**. €25–€50 and US$35–37 are quoted against ADRs of €100–200 and US$125. Harper's ADR is ~RM160 (≈US$34). A late check-out priced at a US benchmark would exceed the room rate. The only defensible approach is to price as a percentage of ADR: **20–30% of ADR, i.e. RM30–50** `(inf.)`.

Modelled conservatively — 12% attach, below the 18–28% vendor band because Harper's guest mix is price-sensitive domestic and OTA and the saleable window is short:

| Item | Attach | Price | Annual |
|---|---|---|---|
| Late check-out | 12% of 3,420 stays | RM40 | **~RM16,400** |
| Early check-in | 8% of 3,420 stays | RM35 | **~RM9,600** |

**A Kota Kinabalu-specific margin note that nobody will tell you.** Since 1 January 2025, DBKK charges hotel licence fees per **occupied** room per day under the Kota Kinabalu City (Hotel & Lodging Houses) By-laws 1966 — RM4.65 Class 1, RM2.65 Class 2, RM1.30 Class 3, with **no fee on unoccupied rooms**. A paid late check-out does not create a new occupied-room-day, so it carries no incremental licence fee. A paid *extra night* does. Late check-out is therefore the cleanest-margin product Harper has: ~100% contribution, no tax other than SST, no licence fee, no commission.

### 2.3 Airport transfers

Kota Kinabalu International is ~8km from the city centre. Observed market pricing: airport shuttle bus RM5; GrabCar roughly RM12–25 depending on source and surge; official airport taxi coupon ~RM30 for up to four people.

A hotel transfer at RM40–60 with an outsourced regular driver yields perhaps **RM15–30 margin** per movement `(inf.)`. At 10% of 3,420 stays that is **~RM6,800/yr**.

**My view: transfers are a service play, not a revenue play, at this scale.** RM6,800 does not justify building anything. What justifies the capability is the arrival-day failure it prevents — a guest met at the airport does not get lost looking for the 4th floor of a commercial block at 23:00. Price it to break even, sell it hard to anyone arriving after 21:00, and book the return as review protection rather than ancillary revenue. Harper already raises airport pickup as a staff request type, so the intake exists; what is missing is the *offer*, which is a pre-arrival capability.

### 2.4 Room upgrades — the asset nobody is using

**Nine room types in a ~40-room property is unusual and it is a genuine commercial asset.** A two-type budget hotel has no upgrade ladder. Harper has eight rungs. Upgrade revenue is the highest-value ancillary available to it, and it is pure contribution: the better room is already cleaned, already in inventory, already costing the same licence fee.

| Item | Value |
|---|---|
| Attach rate | 8% of 3,420 stays `(inf.)` |
| Average nightly uplift between adjacent types | RM40 `(inf.)` |
| Average nights upgraded | 2.5 |
| **Annual** | **~RM27,300** |

That is larger than late check-out and early check-in combined, from the same pre-arrival message.

**And it is the one play that genuinely needs inventory visibility.** You cannot offer an upgrade to a room type you cannot confirm is free. This is the strongest — and in my view the *only* strong — argument for Harper acquiring some form of availability-by-room-type feed. Not a full PMS integration; a daily or twice-daily availability snapshot by type would do. Note the sequencing consequence: upgrades should be built *after* pre-arrival exists, because the pre-arrival message is the delivery vehicle, and the availability work is harder than the template work.

### 2.5 Extended stays — the highest-return transaction in the building

This is the one I would put money on, and it is the one Harper's line is structurally incapable of performing.

An extension is:

- **Zero commission.** Booked direct, by definition, even when the original stay came through Agoda.
- **Zero acquisition cost.** The guest is already in the building and already in the conversation.
- **Near-zero incremental cost.** The room is occupied and being serviced anyway; the only new costs are one night of consumables and the DBKK licence fee (RM1.30–4.65).
- **Full rate.** No OTA promo, no member discount, no parity question — this is not a published rate.

| Item | Value |
|---|---|
| Extension rate | 2% of 3,420 stays `(inf.)` |
| Extra room-nights | ~68 |
| Revenue at RM160 | **~RM10,900/yr** |
| Incremental margin | ~95%+ after consumables and licence fee `(inf.)` |

**And there is a tax fact here that is specific, binding, and directly commercial.** RMCD's *Guide on Digital Platform Service Provider* addresses this exact case at Q3/A3: where a tourist who booked through an OTA extends their stay directly with the hotel, **the accommodation operator must collect the tourism tax for the additional stay** — the platform is not liable unless the extra nights were booked through it. So every extension creates a RM10-per-night TTx collection duty at the desk, plus an invoice that must state TTx separately from the room charge (s.14 Tourism Tax Act 2017; failure carries a maximum RM30,000 fine, RM15,000 compound).

**Which makes the "never states a price" design a revenue problem and a compliance problem at once.** A guest asking "can I stay one more night?" over WhatsApp today gets routed to a website that is built for new bookings, or to a human who may or may not be on shift. The most profitable transaction Harper can make is the one its line is designed never to attempt.

### 2.6 F&B — do not build it

No restaurant on site. There is no F&B upsell to automate and nothing here justifies the effort.

There is an adjacent play worth one line, and it is service rather than revenue: Sutera Avenue is a commercial development with food tenants, and a guest at a property whose desk shut at 22:00 asking "what's still open?" is a high-value question to answer well. A maintained "what's open downstairs now, and what delivers after 23:00" reply earns nothing and prevents a specific category of bad review. Treat it as review protection.

### 2.7 Reduced no-shows — the business case that is not there

I want to be blunt about this one because it is the headline claim in most messaging vendor pitches and it does not survive contact with Harper's numbers.

**The benchmark.** SevenRooms puts hotel room no-shows at **1–2% of bookings** (the page is roughly four years old, so treat it as directional). The same source notes F&B venues run at 20%+ — a completely different problem.

**The evidence usually cited for reminders is from healthcare, and it does not transfer.** A 2020 A/B test across ~161,000 members found an emotionally-framed reminder cut no-shows to 14.2% from 21.1% in control. A Cochrane review of eight randomised trials is cited for text reminders lifting attendance from 67.8% to 78.6%. Both are appointment attendance with 20–30% baseline failure rates. **A 1–2% baseline has essentially no headroom**, and a reminder cannot halve a rate that is already at the floor of operational noise.

| Item | Value |
|---|---|
| No-shows at 1.5% of 3,420 stays | ~51/yr |
| A 20% reduction (optimistic) | ~10 room-nights |
| **Annual value** | **~RM1,600** |

Harper's structure also pushes most of the exposure elsewhere: free cancellation 3 days out and a RM100 cash deposit at check-in (Hostelworld) mean prepaid non-refundable OTA bookings are largely the OTA's problem, and the hotel's real exposure is pay-at-property bookings.

**Conclusion: do not sell the pre-arrival message on no-show reduction.** Sell it on arrival-time capture, tax-and-ID pre-collection, and upsell delivery — all of which are worth multiples of this. Then take the no-show reduction as a free side-effect and do not measure it, because at ~51 events a year you will never distinguish signal from noise.

### 2.8 The money, consolidated

| Revenue line | Annual `(inf.)` | Margin | Confidence |
|---|---|---|---|
| Room upgrades | ~RM27,300 | Very high | Medium — needs availability feed |
| Late check-out | ~RM16,400 | ~100% | Medium-high |
| Extended stays | ~RM10,900 | ~95% | **High — best mechanism, worst current capability** |
| Early check-in | ~RM9,600 | High | Medium |
| Direct-booking deflection (net) | ~RM6,200–8,900 | n/a | Low-medium |
| Airport transfers | ~RM6,800 | Moderate | Medium |
| No-show reduction | ~RM1,600 | n/a | **Very low — ignore** |
| F&B | ~RM0 | n/a | n/a |
| **Total** | **~RM79,000–81,000** | | |

Against ~RM1.37m room revenue that is **roughly 5.8% of topline, at very high margin** — and it lands almost entirely in the three stages where Harper currently does nothing.

**The cost side is a rounding error, and this matters for the decision.** Since 1 July 2025 WhatsApp charges per delivered template message by category, with utility templates **free inside an open customer-service window** and volume tiers on utility and authentication. A third-party rate table (Chatalog — not an official source, currency and effective date not stated) lists Malaysia at US$0.0168 utility and US$0.1032 marketing. On those figures:

| Send | Volume/yr | Unit | Annual |
|---|---|---|---|
| Pre-arrival + arrival-day + post-stay utility templates | ~10,250 | US$0.0168 | ~US$172 (~RM760) |
| One full-base marketing broadcast | 3,420 | US$0.1032 | ~US$353 (~RM1,560) |

**~RM80,000 of accessible margin against roughly RM800–2,500 a year of message cost.** The constraint on this project is not messaging spend. It is template approval, a daily arrivals list, and whether a human closes the loop. Everything in §6 follows from that.

**Ancillary and extension revenue is roughly 10× commission deflection at this scale.** If there is one thing to take from §2, it is that.

---

## 3. What a GM asks on day one

Harper has almost none of this. Each item below states the question, the shape of a good answer, and what is actually there.

### 3.1 Who owns the inbox?

**Harper:** requests become a storage row plus a 1:1 WhatsApp alert to "a staff phone". There is no staff screen.

**Why that is not an owner.** "Whoever is holding that phone" is not a role, and a 1:1 alert is a notification, not an assignment. Nobody can see the queue, nobody can see what another shift left open, and nobody is accountable for an unread message. If the phone-holder is off, the request is in a notification tray nobody opens.

**What is needed:** a named owner per shift against a single shared queue, with the guest conversation and the request visible in the same place. Not a personal device.

**And there is a compliance dimension to this, not just an operational one.** Guest names, arrival dates, room numbers, complaint content and — if ID collection ever starts — passport images are personal data. Routing them to a personal WhatsApp account on a staff member's own handset puts them in that person's message history and their iCloud or Google backup indefinitely, outside Harper's control. Since 1 April 2025 data processors are directly bound by the PDPA's Security Principle, with penalties reported at up to RM1,000,000 or three years. See §4.

### 3.2 What happens at 22:01?

**This is Harper's single largest operational gap and the brief does not frame it as one.**

Assemble the facts: the desk closes at 22:00; reception is on the 4th floor of a multi-block commercial development; KKIA is 8km away and takes late arrivals; the line cannot message first; and the bot is almost certainly not time-aware `(inf.)`. A guest landing at 23:00 who has never been to Sutera Avenue gets a canned reply and a staff alert into a sleeping phone.

**What is needed, in order of cost:**

1. **Time-aware replies.** After 22:00 the line must say what is true: the desk is closed, here is the number to call tonight, here is how to get in. A bot that answers identically at 03:00 is worse than no bot, because it reads as a hotel that does not care.
2. **An explicit after-hours expectation**, stated to the guest, not implied. "Messages are answered from 07:00. For access tonight call X."
3. **A duty phone with a real human** and a defined scope (access, lockout, medical, noise). One person, rostered, paid for it.
4. **A pre-captured late-arrival plan.** The highest-leverage fix is not after-hours staffing — it is asking, 24 hours out, "what time do you land?" and handling the 23:00 answer *before* it becomes a 23:00 problem. That is a pre-arrival capability, which is why §6 ranks pre-arrival first.
5. **The physical answer.** A keypad, lockbox or after-hours access arrangement is the actual fix for a 22:00 desk close, and it is a plant decision, not a software one. Worth saying plainly so that nobody tries to solve a locked door with a chatbot.

### 3.3 How does a request get from the bot to the person holding a mop?

**Harper:** storage row + WhatsApp alert. That is the whole mechanism.

**What is missing is a state machine.** A work order needs states and transitions: `new → assigned → accepted → in progress → done → confirmed to guest`. Harper has `new`, and then an alert, and then hope. There is no acceptance, so nobody knows if it was seen. No timer, so nothing surfaces when it is not. No reassignment, so an absent staffer is a dead end. No completion, so the request is never closed. No confirmation back to the guest, so the guest re-asks — and re-asking is the single strongest predictor of a complaint escalating.

**Minimum viable version for a 40-room property:** one shared queue; a request is claimed by a named person; a timer escalates it if unclaimed; completion sends a line back to the guest in the original thread. That is four behaviours, not a product.

### 3.4 SLAs

There is **no published industry standard**. What exists is a cluster of vendor defaults, and they are consistent enough to use as a starting point:

| Source | Target |
|---|---|
| Oxmaint (maintenance SLA guide) | 15 min life-safety; 30 min in-room failures (HVAC, hot water); 2h non-critical comfort; interval escalation to chief engineer / duty manager |
| Second vendor | 15 min P1; auto-escalate to duty manager at minute 12 if unassigned |
| Housekeeping automation vendor | Unaccepted task → supervisor at 10 min → duty manager at +10 min; VIP arrival tightens to 5 min |
| Guestara (guest messaging) | Acknowledge urgent in-stay requests within 5 min; flag any message unanswered at 10 min |
| Cloudbeds | 73% of travellers prefer messaging to phone; **over 65% expect a response within an hour** |
| Enso Connect | SMS/WhatsApp expectation is ~1 minute to feel "instant" |

**What I would actually set for Harper**, scaled to a 40-room property with a 15-hour desk:

| Scenario | Target |
|---|---|
| First reply, 07:00–22:00 | ≤5 min (bot instant; human ≤5 min on handoff) |
| First reply, 22:00–07:00 | Instant automated acknowledgement stating the real expectation + duty number |
| In-stay request acknowledged | ≤15 min |
| **Noise complaint on site** | **≤10 min** — justified below |
| Routine request completed | ≤2h |
| Complaint escalated to owner/manager | ≤30 min unresolved, or immediately on keyword |

**Noise gets its own tighter SLA because noise is Harper's commercial problem.** It is the top complaint across ~288 reviews. The Cornell study by Chris Anderson (2012) is the canonical link between reputation and rate: a 1% increase in online reputation score was associated with up to **0.89% higher ADR, 0.54% higher occupancy and 1.42% higher RevPAR**. A study of 132 Belgian hotels separately found review *volume* drives occupancy while review *valence* drives RevPAR — and that the effect is stronger in chain and higher-star hotels than in independents and lower tiers, which is a caution for Harper specifically. The secondary "one point on a 5-star scale = 11.2% ADR" figure circulates widely but is a scale conversion applied by third parties, not a direct finding; do not quote it.

The operational consequence is sharp: **the highest-value function of Harper's line is catching the noise complaint while the guest is still in the building.** A noise complaint at 23:30 at a property whose desk closed at 22:00 currently has nowhere to go — so it goes into a review. That is the intersection of Harper's #1 review problem and Harper's #1 operational gap, and it is a cheap thing to fix.

### 3.5 Escalation

Three tiers: bot → on-shift staff → duty manager/owner. Triggers must be more than a timer:

- **Timer:** unacknowledged at N minutes, unresolved at N minutes.
- **Keyword/intent:** refund, police, ambulance, injury, bedbug, theft, "I want to leave", "I want a different hotel", any mention of a review platform.
- **Repeat contact:** the same guest raising the same issue twice is an automatic escalation regardless of timers. This is the cheapest high-yield rule and almost nobody implements it.
- **After-hours:** anything arriving after 22:00 that is not answerable by the time-aware replies.

Harper has human handoff for complaints and refunds, which is tier two. It has no timers, no repeat-contact rule, and no tier three.

### 3.6 Shift handover

Nothing exists. For most hotels handover is a hygiene item; at Harper it is structural, because **at 22:00 the day shift hands over to nobody**. The handover artefact is therefore doing two jobs: passing open items to the morning, and briefing the duty phone on tonight's risk.

**Minimum:** an end-of-shift summary enumerating (a) open requests with age and owner, (b) tonight's expected late arrivals with ETAs, (c) any guest currently unhappy, (d) any room with an unresolved problem. Four lists. It can be a message in a group thread as long as it exists and is written every day.

### 3.7 What gets logged

Harper logs a storage row per request. Here is the full set a property in Kota Kinabalu actually needs, and note how much of it is statutory rather than operational:

| Record | Why | Retention |
|---|---|---|
| Conversation transcript | Dispute resolution, quality, training | Set a policy; PDPA Retention Principle (s.10) requires you not to keep it longer than necessary |
| Request log: type, room, raised, assigned, accepted, completed, confirmed | The only way to compute anything in §5 | Operational |
| Who did what, when | Accountability, handover | Operational |
| Complaint taxonomy incl. a **noise** category with room/floor | Lets you cluster complaints by room and fix the physical cause | Operational |
| **Tourism tax records: guest name and passport number, check-in/check-out dates, room rate, tax amount** | **s.17 Tourism Tax Act 2017** | **7 years, in English or Malay, kept in Malaysia unless the DG approves otherwise.** Failure: max RM30,000 / RM15,000 compound (s.17(5)) |
| TTx invoice stating tax separately from room charge | s.14 TTx Act 2017 | Max RM30,000 / RM15,000 compound (s.14(3)) |
| **Monthly occupied-room declaration to DBKK** | Kota Kinabalu City (Hotel & Lodging Houses) By-laws 1966, reinstated 1 Jan 2025 — fee is per occupied room per day | Ongoing monthly duty |
| PDPA breach register | DBN Guideline | **≥2 years** |
| Marketing consent and opt-out, per guest, with timestamp | PDPA s.43 | For as long as you market |

Two things to notice. First, **"kept in Malaysia" is a real constraint on where a tourism-tax-relevant record may live.** If the only record of a WhatsApp-agreed extension is in a foreign messaging provider's store, that is a question worth asking — though in practice the statutory record is the folio and invoice, not the chat. Second, **the DBKK occupancy declaration is a monthly logging duty that arrived in January 2025 and that a GM will absolutely ask about**, because it is now a five-figure annual cost that scales with occupancy:

| DBKK class | Rate per occupied room/day | Harper at 8,541 occupied room-nights `(inf.)` |
|---|---|---|
| Class 1 | RM4.65 | ~RM39,700/yr |
| Class 2 | RM2.65 | ~RM22,600/yr |
| Class 3 | RM1.30 | ~RM11,100/yr |

Harper's class is unknown to me; a 2.5-star boutique is plausibly Class 2 or 3 `(inf.)`. For context on how large a change this was: operators previously paid around RM10 per room per *year*, and budget hotels reportedly faced a jump from ~RM1,000 to over RM28,000 annually. The Sabah Hotel Association sought a deferral and a RM45 cap; both were rejected, and in April 2025 the state confirmed no deferral. MyBHA and MAH both objected publicly. **This is binding and current.**

### 3.8 What a manager sees weekly

One page. Harper can produce almost none of it today (see §5):

- Conversations, split 07:00–22:00 vs after-hours
- Median and 90th-percentile first response time, same split
- Containment rate (resolved without a human) and handoff rate
- Open requests by age; requests breaching SLA; requests never closed
- **Requests by type, with noise broken out by room and floor**
- Ancillary revenue from the line, and extensions booked
- Escalations, with one line each on what happened
- Unanswered messages — the number nobody wants to publish and the one that matters most

### 3.9 How you prove it is working

**Be honest about statistical power first.** At ~3,420 stays a year — nine arrivals a day — Harper can detect large effects and nothing else. Any claim of a 2-point improvement in anything is noise. This rules out most A/B testing and it rules out all vendor-style attribution modelling `(inf.)`.

What is left is sound and sufficient:

1. **A before/after on things Harper already has.** Review score and the rate of noise mentions in reviews, over quarters not weeks. Direct-booking share from the booking engine. These are lagging and confounded by season — Kota Kinabalu occupancy moved 55.0% → 58.5% year on year independent of anything Harper does — so compare like periods.
2. **A holdout on the one thing worth testing.** Pre-arrival messaging is the only intervention big enough to measure: send to every arrival for a month, suppress for a month, compare ancillary revenue per occupied room and arrival-day incident count. Crude, but at this volume it is the only design with any power.
3. **Counting what cannot be counted today.** The best proof is not a lift; it is the existence of records that did not exist. "Last quarter we captured 31 noise complaints while the guest was in the building; the quarter before, we captured zero and found eleven in reviews." That is not statistics, it is evidence, and for a 40-room hotel it is the right standard.

---

## 4. Compliance and risk in Malaysia

> **Read the research limitation at the top of this document.** The registration-class point and the biometric-data point rest on the DLA Piper *Data Protection Laws of the World* Malaysia chapter (last modified 12 Feb 2026) rather than the gazetted instruments, because the search budget ran out before they could be verified against the Order and the Act. Both are flagged inline. Nothing here is legal advice.

### 4.1 The PDPA, as it now stands

The Personal Data Protection Act 2010 (Act 709) was amended by the **Personal Data Protection (Amendment) Act 2024**, commenced in three tranches. The official instrument list on the Commissioner's site (pdp.gov.my, AKTA 709) confirms the amendment Act, the gazetted commencement order, and the circulars and guidelines named below.

| Tranche | Date | What started |
|---|---|---|
| 1 | 1 Jan 2025 | Ancillary only — rectification of the Malay text, service of documents. **No new obligations on controllers** |
| 2 | 1 Apr 2025 | Cross-border transfer (amended s.129); **data processors directly bound by the Security Principle** |
| 3 | 1 Jun 2025 | Breach notification (s.12B), DPO appointment, data portability (s.43A) |

**Instruments that matter:**

- **Circular of the Personal Data Protection Commissioner No. 1/2025 (Data Breach Notification)** — dated 25 Feb 2025, in force 1 Jun 2025 — plus the *Personal Data Protection Guidelines on Data Breach Notification (DBN)*.
- **Circular No. 2/2025 (Appointment of Data Protection Officer)** plus the *Guidelines on the Appointment of Data Protection Officer (DPO)*.
- **Personal Data Protection Guidelines on Cross-Border Transfer of Personal Data (CBPDT)**, issued 29 Apr 2025.
- **Circular No. 1/2026 (Registration of Data Controllers)** — newer than most commentary and worth reading directly.

### 4.2 What is genuinely binding on Harper

| # | Obligation | Binding on Harper? | Detail |
|---|---|---|---|
| 1 | **Register as a data controller with the Commissioner** | **Yes — and most easily missed** | The mandatory registration classes include **operators of registered tourist accommodation premises under the Tourism Industry Act 1992**. Certificates are valid for at least a year, must be renewed, must be displayed at the principal place of business with certified copies at branches, and **processing may not continue after expiry**. ⚠ Per DLA Piper, not verified against the Class of Data Users Order. See Circular 1/2026 |
| 2 | **Tourism tax: collect, invoice, return, retain** | **Yes** | Registered if ≥5 rooms, within 30 days of commencing (ss.10–11 TTx Act 2017). RM10/room/night. Invoice must state TTx separately (s.14). Records 7 years, in Malaysia (s.17). Form TTx-03, quarterly for non-GST operators, due by the last day of the month after the taxable period (s.19). Each failure: max RM30,000 / RM15,000 compound (s.56) |
| 3 | **DBKK monthly occupied-room declaration and licence fee** | **Yes** | By-laws 1966, reinstated 1 Jan 2025. RM4.65 / RM2.65 / RM1.30 per occupied room/day by class; no fee on unoccupied rooms |
| 4 | **Service tax at 8% on accommodation** | **Yes, almost certainly** | Registration threshold RM500,000; Harper at ~RM1.37m room revenue is over it `(inf.)`. Rate raised from 6% to 8% from 1 Mar 2024 (Service Tax (Rate of Tax) (Amendment) Order 2024, P.U.(A) 64/2024). One source lists accommodation at 6%; 8% is better supported — **verify on the RMCD MySST portal** |
| 5 | **Breach notification** | **Yes, when triggered** | s.12B. Notify the Commissioner as soon as practicable and **within 72 hours** where the breach causes or is likely to cause significant harm; affected individuals **within 7 days** of notifying the Commissioner. "Significant harm" includes financial loss, misuse for illegal purposes, sensitive data, identity-fraud risk. **>1,000 affected data subjects** is "significant scale" for the Commissioner notice only. Keep a **breach register ≥2 years**. Notification is via the pdp.gov.my form or the Annex B form |
| 6 | **Security Principle, including on processors** | **Yes, and on vendors** | From 1 Apr 2025 processors are **directly** bound, with penalties reported at up to **RM1,000,000 or 3 years**. Any BSP, cloud host or agency touching Harper's guest data is now liable in its own right — which is also a contracting lever |
| 7 | **Cross-border transfer** | **Yes, in practice** | Amended s.129 from 1 Apr 2025. The whitelist is gone (and was never populated). Transfer is permitted where the destination has a substantially similar law **or** ensures equivalent protection; fallbacks include consent, contract necessity and reasonable precautions. The CBPDT Guidelines require a **Transfer Impact Assessment** for adequacy-based transfers and recognise BCRs, SCCs and approved certifications. Unlawful transfer penalty reportedly unchanged at RM300,000 / 2 years (s.129(5)). **This bites: WhatsApp/Meta, any non-Malaysian BSP, and any staff phone backing up to iCloud or Google all move guest data offshore.** Commentary conflicts on which subsections were deleted — check Act A1727 |
| 8 | **Retention Principle** | **Yes** | s.10. No standalone right to erasure, but a positive duty not to keep data longer than necessary. This is the provision that makes "we keep every WhatsApp thread forever" a problem |
| 9 | **Direct marketing opt-out** | **Yes, the moment marketing starts** | s.43: a data subject may give written notice to stop or not begin processing for direct marketing; the controller must stop within a reasonable period and must not resume without fresh consent. Non-compliance with a Commissioner direction: fine up to **RM200,000 and/or 2 years** (s.43(4)) |
| 10 | **Officer liability** | **Yes, personally** | Directors, CEOs, managers and similar officers are **jointly and severally liable** for the body corporate's non-compliance, subject to a due-diligence defence. For an owner-operated boutique this is personal exposure, not corporate |

### 4.3 What is NOT binding — and the money this saves

**A DPO is probably not mandatory.** The thresholds are: personal data of **more than 20,000 data subjects**; sensitive personal data including financial information of **more than 10,000**; or **regular and systematic monitoring**. Harper handles roughly 3,420 stays a year — perhaps 5,000–7,000 individuals — so on an annual-processing reading it is well under, and on a cumulative-database reading it would take years to cross 20,000 `(inf.)`. A WhatsApp line answering questions is not "regular and systematic monitoring" on any natural reading `(inf.)`.

**Do not appoint and register a DPO on the assumption that the law requires it.** Check the threshold against actual record counts first. Note that if one *is* appointed, further duties attach: notify the Commissioner **within 21 days**, publish the DPO's business contact details on the website or in the privacy notice, keep appointment records, and the DPO must be proficient in Malay and English and resident in Malaysia or easily contactable.

**Electronic marketing is not yet separately regulated.** The PDPA contains no specific electronic-marketing provision beyond s.43. An MCMC framework consulted on 13 August 2025 **would** require consent, allow implied consent only on an established relationship, and mandate a free unsubscribe mechanism — **but it is not in force.** Build the opt-out anyway; it is coming and s.43 requires honouring opt-outs regardless.

### 4.4 Photos of identity documents over WhatsApp — the sharpest practical item

This is the question Wilfred asked specifically, and it has a clean answer.

**Classification.** The 2024 amendment added **biometric data** to the definition of sensitive personal data in s.4, defined as personal data resulting from technical processing of physical, physiological or behavioural characteristics. A photograph of a passport data page is an image, not the output of technical processing, so on a plain reading it is **personal data but not sensitive personal data** `(inf.)`. That changes if the image is ever run through face matching, at which point the derived template plainly is biometric. ⚠ This classification rests on the DLA Piper summary of the amended definition, not the gazetted s.4 text.

**But classification is not the real risk. Location and lifetime are.** A passport image sent to a WhatsApp number lands in at least four places, three of which Harper does not control:

1. The guest's own device.
2. Harper's WhatsApp message history, indefinitely, with no retention rule.
3. The business solution provider's media store — offshore, which is a **cross-border transfer under amended s.129** that nobody has assessed and for which no Transfer Impact Assessment exists.
4. If the receiving handset is a personal staff phone, that staffer's **iCloud or Google backup** — a second, invisible, unassessed offshore transfer, on a device Harper cannot wipe when the staffer leaves.

That is a Security Principle problem (s.9), a Retention Principle problem (s.10) and a cross-border problem (s.129) from one photograph.

**And here is the finding that resolves it cheaply: Harper has no lawful need to keep the image at all.** Section 17 of the Tourism Tax Act 2017 requires the operator to preserve the **name and passport number** of the tourist, the check-in and check-out dates, the room rate and the tax amount. It does not require an image of the document. So the defensible policy is a single rule:

> **Transcribe the number. Delete the image. Never from a personal device.**

Concretely: (a) do not solicit ID images over WhatsApp unless there is a specific need that the desk cannot meet; (b) if one arrives, transcribe name and passport number into the TTx record and delete the message and any media copy; (c) state the retention rule in the privacy notice; (d) never receive them on a personal handset — which is an independent argument for §6's shared staff queue; (e) if images must be retained for any reason, document the purpose, the retention period and a Transfer Impact Assessment for wherever they are stored.

Note that the two records here have different lifetimes and must not be conflated: the **TTx record** lives 7 years, in Malaysia. The **image** should live minutes.

### 4.5 Tourism tax: the three operational traps

The RM10 per room per night is simple. Three interactions with a messaging line are not.

**Trap 1 — the exemption is not universal, and a bot that says it is will mis-collect.** Under paragraph 2 of the Tourism Tax (Exemption) Order 2017, **Malaysian nationals and permanent residents (MyPR holders) are exempt from the whole of TTx.** Harper's listings advertise "a MYR10 nightly tourism fee paid at the property" (Hostelworld). A canned reply that states the fee without the exemption is wrong for roughly two-thirds of Harper's guests, given the national 64% domestic split. It also means the exemption decision requires sighting nationality at the desk — which is the legitimate reason ID is checked, and an argument for capturing it pre-arrival rather than in a queue.

**Trap 2 — the OTA proof problem, which pre-arrival is the natural place to solve.** Under paragraph 8 of RMCD's DPSP guide: where TTx for an online booking has been paid by the tourist to the platform, **the registered operator need not collect it — provided the tourist submits proof of that payment.** No proof, and the operator must collect and remit. The guide's Example 2 has a Langkawi resort charging RM60 TTx at check-out because the platform took nothing. Platform practice differs: Q1/A1 has the platform collecting; Q2/A2 has the platform liable even where the hotel collects the room rate directly; Example 4 has a reservation-only platform leaving both room charge and TTx to the hotel.

For Harper — "a lot of OTA bookers" across Agoda, Booking.com and Trip.com — this is a daily desk argument and a recurring collection gap. **A pre-arrival message asking OTA bookers to send their booking confirmation showing TTx would resolve it before the guest is standing at the desk.** Harper sends nothing pre-arrival, so every unproved OTA booking is settled by negotiation at check-in, and the exposure sits with the hotel.

**Trap 3 — extensions, covered in §2.5.** Q3/A3 is explicit: the operator collects TTx for nights added directly. So the most profitable WhatsApp transaction available also creates a tax duty, an invoice duty (separately stated, s.14) and a record duty (s.17).

### 4.6 One accidental virtue of the current design

**"It never states a price" is, right now, a compliance asset.** A correct quote at Harper is room rate **+ 8% service tax + RM10 per room per night TTx if the guest is a foreign national**, and the invoice must state the TTx separately. A bot that confidently quoted "RM160 a night" would understate the bill, generate desk disputes, and risk s.14 exposure if what followed was not a compliant invoice.

So: the fix in §6 is not "let the bot quote." It is **"let the bot quote correctly, with tax components stated and a compliant invoice issued."** Pricing capability and tax correctness have to ship together.

### 4.7 Also worth naming, not binding on the line

- **Tourism Industry Act 1992 (Act 482), s.31A** — an operator of accommodation premises must apply to the Commissioner to register the premises as tourist accommodation premises. This is the registration that **triggers PDPA registration class membership** (§4.2 item 1), so the two are linked. S.31D is headed "Register", but its text was not retrievable within budget; if a statutory guest-register duty exists it sits there and is worth checking.
- **MyCC identified a regulatory gap**: foreign digital-first OTAs are not covered by the Tourism Industry Act 1992, which reaches only OTAs with a physical presence in Malaysia. Harper is regulated; the platforms taking 17–20% of its revenue partly are not.

---

## 5. Metrics

### 5.1 What the line should be measured on

| Metric | Definition | Credible benchmark | Harper today |
|---|---|---|---|
| First response time | Median and p90 to first *useful* reply, split day/after-hours | >65% of travellers expect a reply within 1h (Cloudbeds); 1 min reads as instant on WhatsApp (Enso); vendor default 5 min urgent | **Computable** from message timestamps |
| Containment rate | Resolved with no human | No credible hospitality benchmark found | **Computable** if handoffs are flagged |
| Handoff rate | Share escalated to a human | — | **Computable** |
| Unanswered rate | Guest messages with no reply at all | Should be ~0 | **Computable, and should be the first thing anyone looks at** |
| After-hours share | Conversations 22:00–07:00 | — | **Computable — and will be the most revealing number Harper has** |
| Request fulfilment time | Raised → completed | Vendor defaults: 15 min P1, 2h routine | **Not computable** — no completion state exists |
| Closure rate | Requests confirmed back to the guest | — | **Not computable** |
| Pre-arrival reach | Arrivals contacted before arrival | — | **0%, and not computable** — no arrivals list |
| Ancillary revenue per occupied room | Line-attributed ancillary ÷ occupied room-nights | Hotel-wide analogue: US parking revenue US$11.53 per occupied room in 2023, +23.1% vs 2019 — different product, cited for the unit | **Not computable** — no price, no attribution |
| Upsell conversion | Offers accepted ÷ offers made | 8–15% pre-arrival; 18–28% late check-out; 15–30% monetised ECI/LCO — **all vendor, unattributed, see §2.2** | **Not computable** — no offers are made |
| Extension rate | Stays extended ÷ stays | — | **Not computable** |
| Direct-booking share | Direct ÷ total room-nights | Independents gave 63.4% to OTAs in 2025 (Cloudbeds, via secondary) | Partly — from the booking engine, not attributable to the line |
| Review score and volume | Platform scores; reviews per 100 occupied room-nights | Anderson/Cornell 2012: +1% reputation ≈ +0.89% ADR, +1.42% RevPAR. Belgian 132-hotel study: volume→occupancy, valence→RevPAR, **weaker in independents and lower star tiers** | Manually; **no review ingestion** |
| **In-stay complaint capture** | In-stay complaints ÷ (in-stay complaints + complaints appearing only in reviews) | None published | **Not computable** — needs both a complaint taxonomy and review ingestion |
| Cost per conversation | Message + staff cost ÷ conversations | Message cost ~US$0.0168 utility / US$0.1032 marketing (Malaysia, third-party table) | **Computable for messages**; staff time is the real cost and is unmeasured |

### 5.2 What Harper can actually compute today

Short list, and worth stating plainly because it bounds any reporting promise:

- Message and conversation volume
- Time to first reply (from timestamps)
- Request counts by type
- Language mix (Malay / English / Chinese)
- After-hours volume
- Handoff counts, if handoffs are marked

**That is all.** Everything revenue-side, everything fulfilment-side and everything lifecycle-side is uncomputable, because there is no PMS join, no checkout event, no price, no attribution and no review feed. A weekly manager report built on today's data can describe traffic and nothing else.

### 5.3 The one metric for the wall

> **Noise complaints we heard while the guest was still here — per 100 occupied room-nights, weekly.**

Why this one, over the obvious candidates:

- **It is the only metric that connects the line to the property's actual commercial problem.** Noise is the top complaint across ~288 reviews; review valence maps to ADR and RevPAR through the Cornell relationship. Response time does not appear anywhere in that chain. This does.
- **It is computable from the request log alone**, as soon as a `noise` request type exists with a room number. No PMS, no revenue attribution, no review scraping.
- **Its success condition is counter-intuitive in a way that teaches the team the right thing.** It should go **up** first. A rising count means complaints are reaching the hotel instead of TripAdvisor. The win shows up as a *second* line falling behind it: noise mentions in new reviews. Put both on the wall and let staff watch them cross. Nothing else makes "we want to hear more complaints" an intelligible goal to a front-desk team.
- **It drives the right behaviour at the right hour.** You cannot move this number without someone reachable at 23:30, which is exactly the capability Harper lacks.

Runner-up, for the manager's own dashboard rather than the wall: **after-hours conversation share**. It will be larger than anyone expects, and it is the single most economical argument for the duty-phone and time-aware-reply work in §6.

---

## 6. The ranked list

Ordered by return against effort for a ~40-room, 9-room-type boutique. Each item states the return, the effort, and why it sits where it does.

### 6.1 Build, in this order

**1. Pre-arrival message: arrival-time capture, directions, after-hours plan, OTA tax proof — plus one upsell.**

*Return: very high. Effort: low-to-moderate — the gate is template approval plus a daily arrivals list, not engineering.*

This is first and it is not close. The reasoning, since Wilfred asked for it on the top item specifically:

- **It is the only item that unlocks the others.** Pre-arrival, post-stay and next-stay are absent for the same two reasons (§1.3): no ability to initiate, no event feed. The work to fix those two things is shared across all three stages. Doing pre-arrival first buys the enabling layer and the highest-value stage in one pass. Doing anything else first buys one feature.
- **It defuses Harper's worst failure mode before it happens.** The 22:00 desk close plus a 4th-floor reception in a commercial block plus late KKIA arrivals produces the lost-guest incident that writes one-star reviews. You cannot staff your way out of it economically at 40 rooms. You *can* ask "what time do you land?" 24 hours ahead and handle the 23:00 answers deliberately. That converts an emergency into a scheduled task.
- **It is the delivery vehicle for the revenue in §2.** Upgrades (~RM27,300), late check-out (~RM16,400) and early check-in (~RM9,600) are all pre-arrival or arrival-morning offers. Without an outbound message there is no channel for any of them. Roughly RM53,000 of the ~RM80,000 total sits downstream of this one capability.
- **It closes the tourism-tax collection gap** (§4.5 trap 2) by asking OTA bookers for proof of TTx payment before they reach the desk, instead of negotiating it at check-in.
- **It is almost free to run.** ~3,420 utility templates a year is roughly RM270 at Malaysian utility rates, and utility templates inside an open customer-service window cost nothing.
- **And the cheap version is genuinely cheap.** A manually pasted or exported arrivals list and one approved template delivers most of the value. The expensive version — a PMS or channel-manager integration — delivers the same message with a six-month tail. Do the cheap version now; see §6.2.

**2. Let the line state a price and close — extensions and late check-out first.**

*Return: high. Effort: moderate. Must ship with tax correctness.*

Extensions are the highest-margin transaction in the building: full rate, zero commission, zero acquisition cost, room already serviced (§2.5). Late check-out is ~100% contribution and carries no incremental DBKK licence fee (§2.2). Both are blocked by one design decision: the line never states a price.

Ship with the tax components, not after them — rate + 8% SST + RM10/night TTx for foreign nationals only, separately stated, with a compliant invoice following (§4.6). And handle the parity question first: confirm against Harper's actual Agoda and Booking.com agreements whether a one-to-one quoted rate is treated as a closed-user-group rate (§2.1).

**3. One shared staff queue with assignment, acknowledgement, timer and closure.**

*Return: moderate directly, high as an enabler. Effort: moderate.*

This earns nothing by itself. It is here at three because items 1, 2 and 5 are not trustworthy without it — you cannot promise a pre-arrival upsell you cannot fulfil, and you cannot ask for a review you have not earned. It also removes guest personal data from personal handsets, which is the cheapest Security Principle and cross-border risk reduction available (§3.1, §4.4). Four behaviours, not a product: claim, acknowledge, escalate on timer, confirm back to the guest.

**4. After-hours mode: time-aware replies, stated expectations, duty-phone path.**

*Return: high on review protection. Effort: low.*

Mostly configuration, not construction. A line that says what is true after 22:00 and routes real emergencies to a rostered human. Partly pre-empted by item 1 — the best after-hours fix is pre-arrival capture — but the residual matters because not every guest answers a pre-arrival message. Note again that a keypad or lockbox is the actual answer to a locked door, and that is a plant decision (§3.2).

**5. Post-stay: review ask, with the low-score interception.**

*Return: moderate-to-high but lagging. Effort: low once item 1's plumbing exists.*

Review volume maps to occupancy and valence to RevPAR (Anderson/Cornell 2012; the 132-hotel Belgian study), and volume drives OTA ranking. The pattern that matters: ask privately first, route unhappy responses to a manager, invite happy ones to post publicly. Requires the s.43 opt-out machinery to be real before anything resembling marketing goes out (§4.2 item 9), and will need the MCMC consent framework watched (§4.3).

**6. Noise-specific intake with room-level clustering.**

*Return: high relative to effort. Effort: very low.*

A `noise` request type carrying room and floor, and a weekly cluster view. This is the metric on the wall (§5.3) and it is cheap enough to fold into item 3. It is listed separately only so it does not get dropped, and it would be defensible to promote it above item 5. Its real payoff is physical: clustering tells you whether the problem is one wall, one floor, or the building, and that is a capex conversation you cannot currently have with evidence.

**7. Upgrade offers.**

*Return: highest single revenue line (~RM27,300). Effort: high — gated on availability by room type.*

Last among the builds despite the largest number, because it is the only item that cannot be done without knowing what is free. Nine room types is Harper's best commercial asset and the hardest to use. A twice-daily availability snapshot by type is enough; a full PMS integration is not required. Park it until items 1 and 3 exist, then revisit — the gate is data, not demand.

### 6.2 Do not build

A 9-room-type boutique with nine arrivals a day should not build what a 400-room chain builds. Specifically:

| Do not build | Why not |
|---|---|
| **A PMS or booking-engine integration as step one** | A manually exported arrivals list gets most of pre-arrival's value this month. The integration gets the same message live next quarter. Sequence it after the message is proven to work, not before |
| **Dynamic pricing or AI revenue management** | 40 rooms, 9 types, one market, one seasonality pattern. The optimisation surface is a spreadsheet. The ADR gap between Sabah's RM344.70 state average and Harper's ~RM160 is a positioning question, not an algorithm |
| **A loyalty programme with tiers or points** | At ~3,420 stays a year, "loyalty" is remembering a returning guest's name and preference and giving them a direct rate. That is a stored preference and one template, not a programme. Tiers also create marketing-consent obligations you do not need yet |
| **F&B ordering** | No restaurant. Maintain a "what's open downstairs" reply instead and treat it as review protection (§2.6) |
| **Multi-channel expansion (Instagram, WeChat, webchat, Line)** | Not until the WhatsApp line closes a single request end to end. Adding channels multiplies an unfinished fulfilment loop. WhatsApp reach among Malaysian internet users is ~90%; the channel is not the constraint |
| **Mobile key / contactless check-in** | The problem at 22:01 is not a key, it is a building — finding the right block, lift and floor with nobody to ask. Solve presence and directions first. The physical access fix is a keypad, which is capex, not software |
| **No-show reduction as a project** | 1–2% base rate, ~51 events a year, ~RM1,600 of theoretical upside you cannot reliably capture, and no statistical power to prove it either way (§2.7). Take it as a side-effect of item 1 and never report on it |
| **More canned replies** | 43 already exceeds what the question distribution needs. The gap is not coverage — it is initiation and closure. Reply number 44 moves nothing |
| **A DPO appointment "to be safe"** | Thresholds are >20,000 data subjects, >10,000 with sensitive data, or regular systematic monitoring. Harper is very likely under all three `(inf.)`. Appointing one creates registration, publication and record duties you were not carrying (§4.3). Check the counts first |
| **Storing passport or IC images** | Transcribe the number for the TTx record, delete the image. The statute wants the number, not the picture (§4.4) |
| **Sentiment dashboards and conversation analytics** | At nine arrivals a day the n is too small for anything but counting. Count noise complaints and unanswered messages; skip the analytics layer entirely |
| **Chasing commission deflection as the headline business case** | Worth under RM9,000 a year net at this scale, against ~RM70,000 in ancillary and extension revenue (§2.8). Leading with it sets up the wrong scoreboard and the wrong roadmap |

---

## 7. Sources

**Primary / official**

- Personal Data Protection Department Malaysia (JPDP), Act 709 instrument list — Act, Personal Data Protection (Amendment) Act 2024, gazetted commencement order, Circulars 1/2025 (Data Breach Notification), 2/2025 (Appointment of DPO), 1/2026 (Registration of Data Controllers), and the DBN, DPO and CBPDT Guidelines: https://www.pdp.gov.my/ppdpv1/en/akta709/
- Royal Malaysian Customs Department, *Guide on Tourism Tax (Digital Platform Service Provider)*, as at 13 August 2021 — paras 7–12, Q1–Q7 (text extracted locally): https://www.myttx.customs.gov.my/wp-content/uploads/2022/05/Guide-on-tourism-tax-DPSP-1.pdf
- Royal Malaysian Customs Department, *General Guide on Tourism Tax*, as at 17 May 2018 — registration (paras 27–35), invoice and records (paras 36–53), returns (paras 54–58), compoundable offences (para 72), Tourism Tax (Exemption) Order 2017 paras 2–3 (text extracted locally): https://www.myttx.customs.gov.my/wp-content/uploads/2022/05/APPENDIX-A-General-Guide.pdf
- Tourism Malaysia, *Paid Accommodation Survey Performance, January–September 2025*, Strategic Planning Division, updated 3 December 2025 — occupancy and average room rate by state and locality (text extracted locally): https://data.tourism.gov.my/frontend/pdf/Infographic-paid-accommodation-survey-performance-jan-sept-%202025.pdf
- Tourism Industry Act 1992 (Act 482), updated reprint, Attorney General's Chambers: https://lom.agc.gov.my/ilims/upload/portal/akta/outputaktap/1684998_BI/Act%20482%20(Muktamad).pdf
- Malaysia Competition Commission, *Market Review on the Digital Economy Ecosystem under the Competition Act 2010* — Book 4, Online Travel Agencies (landing page; the PDF is behind Cloudflare and could not be retrieved): https://www.mycc.gov.my/market-review/online-travel-agencies-market-review-on-the-digital-economy-ecosystem-under-the
- WhatsApp Business Platform pricing (per-message model from 1 July 2025): https://developers.facebook.com/docs/whatsapp/pricing

**Legal commentary**

- DLA Piper, *Data Protection Laws of the World* — Malaysia (last modified 12 Feb 2026). Source for the mandatory registration classes including operators of registered tourist accommodation premises, biometric data in the s.4 sensitive-data definition, s.12B breach notification, DPO thresholds, s.129 and the CBPDT Transfer Impact Assessment requirement, s.43 direct marketing, and officer liability: https://www.dlapiperdataprotection.com/?t=law&c=MY
- DLA Piper Privacy Matters, *Malaysia: Guidelines Issued on Data Breach Notification and Data Protection Officer Appointment*, 4 March 2025 — DPO thresholds, 21-day notification, 72-hour and 7-day breach rules, 2-year breach register: https://privacymatters.dlapiper.com/2025/03/malaysia-guidelines-issued-on-data-breach-notification-and-data-protection-officer-appointment/
- Rödl & Partner, *Part 3: Personal Data Protection (Amendment) Act 2024 — Cross Border Personal Data Transfer Guidelines* (CBPDT issued 29 April 2025): https://www.roedl.com/en/insights/malaysia-part3-personal-data-protection-amendment-act-2024/
- Transatlantic Law International, *Countdown to Compliance: Personal Data Protection (Amendment) Act 2024 in Force 1 January 2025* — three-tranche commencement: https://www.transatlanticlaw.com/content/malaysia-update-countdown-to-compliance-personal-data-protection-amendment-act-2024-in-force-1st-january-2025/
- Donovan & Ho, *Guideline on Data Breach Notification 2025*: https://dnh.com.my/guideline-on-data-breach-notification-2025-guideline/
- Donovan & Ho, *Direct Marketing and Personal Data Protection in Malaysia* — s.43 and s.43(4) penalties: https://dnh.com.my/direct-marketing-and-personal-data-protection-in-malaysia/
- Chambers, *Data Protection & Privacy 2026 — Malaysia, Trends and Developments*: https://practiceguides.chambers.com/practice-guides/data-protection-privacy-2026/malaysia/trends-and-developments/O24504
- Richard Wee Chambers, *MyCC: A Market Review on the Digital Economy Ecosystem under the Competition Act 2010* — commission ranges 10–18% (chains) and 17–20% (smaller hotels), parity findings, Tourism Industry Act 1992 coverage gap: https://www.richardweechambers.com/malaysia-competition-commission-mycc-a-market-review-on-the-digital-economy-ecosystem-under-the-competition-act-2010/
- Legal Dive, *Online price parity clauses at risk after EU Booking.com decision* (CJEU Case C-264/23): https://www.legaldive.com/news/online-price-parity-clauses-at-risk-eu-bookingcom-decision-lodging-other-industries/727688/

**Tax**

- Wolters Kluwer Malaysia, service tax rate change context (Service Tax (Rate of Tax) (Amendment) Order 2024, P.U.(A) 64/2024): https://www.wolterskluwer.com/en-my/expert-insights/rental-and-leasing-services-now-subject-to-8-percent-service-tax
- Mysoftinn, *Malaysia Hotel Tax 2025* — accommodation at 8%, RM500,000 threshold: https://page.mysoftinn.com/en/malaysia-hotel-tax-2025
- Malay Mail, *Hotel group says Budget 2024 service tax hike adds speed bump to hospitality industry recovery* — 6%→8%: https://www.malaymail.com/news/malaysia/2023/10/13/hotel-group-says-budget-2024-service-tax-hike-adds-speed-bump-to-hospitality-industry-recovery/96149
- Agoda Partner Hub, *Malaysian Tourism Tax FAQs*: https://partnerhub.agoda.com/malaysian-tourism-tax-faqs/

**Kota Kinabalu licence fees**

- Daily Express, *DBKK reinstates the original hotel fees* — Kota Kinabalu City (Hotel & Lodging Houses) By-laws 1966, effective 1 January 2025, RM4.65 / RM2.65 / RM1.30 per occupied room per day, no fee on unoccupied rooms: https://www.dailyexpress.com.my/news/250288/dbkk-reinstates-the-original-hotel-fees/
- The Vibes, *Sabah to enforce revised hotel license fees despite objections* — rates, prior RM10/room/year, RM1,000→RM28,000 budget-hotel estimate, RM45 cap request rejected: https://www.thevibes.com/articles/news/107052/sabah-to-enforce-revised-hotel-license-fees-despite-objections
- Malay Mail, *Kota Kinabalu City Hall re-enforces hotel licence fees effective Jan 1*: https://www.malaymail.com/news/malaysia/2025/01/16/kota-kinabalu-city-hall-re-enforces-hotel-licence-fees-effective-jan-1-industry-players-warn-of-potential-cost-impacts/163477
- Malaysian Association of Hotels, *Press Statement — Response to Kota Kinabalu Hotels Licensing Fees Hike*: https://www.hotels.org.my/article/27394-press-statement-response-to-kota-kinabalu-hotels-licensing-fees-hike
- Bernama, *Revised Hotel Licensing Fees In Kota Kinabalu To Proceed*: https://www.bernama.com/en/general/news.php?id=2413279

**Competition / OTA commentary**

- The Star, *Govt identifies anti-competitive practices among online travel agencies, says Armizan*, 10 February 2026 — minister's statement on parity clauses, 18 recommendations, SToDS RM1.62bn in 2024: https://www.thestar.com.my/news/nation/2026/02/10/govt-identifies-anti-competitive-practices-among-online-travel-agencies-says-armizan
- Stayfarer, *OTA commission rates Malaysia 2026* — Booking.com 15–18% before paid programmes, 18–30% all-in; 8% service tax on digital services on top: https://stayfarer.com/guides/ota-commissions
- HotelsSEO, *OTA vs Direct Booking Cost Statistics* — direct acquisition 5–12%: https://hotelsseo.com/resources/statistics/ota-vs-direct-booking-cost-statistics
- Pixel & Polish, *The Boutique Hotel Direct Booking Benchmark* — 9% median all-in direct cost: https://pixelandpolish.com/folio/the-boutique-hotel-direct-booking-benchmark
- Sojern, *Hotel Direct Bookings vs OTA Fees* — Kalibri Labs figures: https://www.sojern.com/blog/how-to-get-more-hotel-bookings-on-otas-and-why-you-might-not-need-to

**Upsell, ancillary and messaging benchmarks (vendor-published — see caveats in §2.2)**

- Stayntouch, *Hotel Ancillary Revenue Strategies: An Operator's Playbook*: https://www.stayntouch.com/articles/hotel-ancillary-revenue-strategies
- Stayntouch, *Maximize Hotel Revenue with Automated Upsells*: https://www.stayntouch.com/articles/maximize-hotel-revenue-upsells
- Revenue Hub, *Fact: Guests Will Buy an Early Check In and Late Check Out* — ROOMDEX single-property case: https://revenue-hub.com/fact-guests-will-buy-an-early-check-in-and-late-check-out/
- Cloudbeds, *Hotel Guest Messaging* — 73% prefer messaging, >65% expect a reply within an hour: https://www.cloudbeds.com/hotel-guest/messaging/
- Enso Connect, *Response Times in Hospitality*: https://ensoconnect.com/resources/response-times-in-hospitality-a-guide-for-vacation-rental-professionals
- Guestara, *Hotel Guest Message Response Time: Benchmarks and Best Practices*: https://www.guestara.com/post/hotel-guest-message-response-time-benchmarks
- Oxmaint, *Hotel Maintenance SLA Guide*: https://oxmaint.com/industries/hospitality/hotel-maintenance-request-response-time-sla
- OwnMyHotel, *Housekeeping Automation* — 10-minute escalation ladder: https://ownmyhotel.com/blog/housekeeping-automation
- SevenRooms, *How to Reduce & Handle Hotel No-Shows* — 1–2% hotel no-show rate: https://sevenrooms.com/blog/reduce-handle-hotel-no-shows/

**Reputation and revenue research**

- Anderson, C.K. (2012), Cornell Center for Hospitality Research — +1% reputation score ≈ +0.89% ADR, +0.54% occupancy, +1.42% RevPAR, as cited in: https://www.inhotel.io/blog/how-much-do-guest-ratings-really-influence-hotel-revenue
- *The Impact of Online Reviews on Hotel Performance* — 132 Belgian hotels; volume→occupancy, valence→RevPAR, weaker in independents and lower star tiers: https://www.researchgate.net/publication/376219166_The_Impact_of_Online_Reviews_on_Hotel_Performance
- Hospital messaging A/B test (2020), ~161,000 members — 21.1%→14.2% no-shows with emotionally framed reminders. **Healthcare, not hotels**: https://www.ncbi.nlm.nih.gov/pmc/articles/PMC7310733/

**Property and market context**

- Hostelworld, Harper Boutique Hotel — check-in 15:00, check-out 12:00, RM100 cash deposit, MYR10 nightly tourism fee paid at property, free cancellation 3 days before arrival, "45 cozy rooms": https://www.hostelworld.com/hotels/p/340387/harper-boutique-hotel/
- Trip.com, Harper Boutique Hotel at Sutera Avenue — 38 rooms, 4.4/5 from 202 reviews, 2.5-star, guest review praising WhatsApp communication: https://se.trip.com/hotels/kota-kinabalu-hotel-detail-73366173/harper-suite-at-sutera-avenue/review.html
- tiket.com, Harper Boutique Hotel — 38 rooms: https://www.tiket.com/en-us/hotel/malaysia/harper-boutique-hotel-908001785657772310
- DataReportal, *Digital 2025: Malaysia* — 34.9m internet users, 97.7% penetration, 25.1m social media identities: https://datareportal.com/reports/digital-2025-malaysia
- Cities Insider, Kota Kinabalu transport costs — Grab airport–city RM12–18, airport taxi coupon ~RM30, shuttle RM5: https://citiesinsider.com/country/Malaysia/kota-kinabalu/guides/kota-kinabalu-transport/en
- Southeast Asia Backpacker, Kota Kinabalu airport guide — ~8km, shuttle RM5: https://southeastasiabackpacker.com/airport-kota-kinabalu/
- Chatalog, WhatsApp conversation fees 2025 — Malaysia per-message rates (**third-party, currency and effective date not stated**): https://chatalog.ai/en/pricing-whatsapp-conversation-fees-2025/
