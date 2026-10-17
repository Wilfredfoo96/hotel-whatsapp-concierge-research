# Market Teardown: Commercial Hotel Guest-Messaging Products vs Harper

**Scope.** Competitive product teardown of what hotel guest-messaging bots actually ship, benchmarked against Harper Boutique Hotel's WhatsApp concierge (Kota Kinabalu, Sabah; 9 room types; no on-site restaurant; reception on the 4th floor of a commercial building; WhatsApp Business Platform via Meta Cloud API through Kapso, Cloudflare Worker logic, Claude as fallback only).

**Date of research.** 16 October 2026. All prices and feature gates are as published on that date.

**Method.** Vendor feature/pricing/integration pages, Hotel Tech Report category and head-to-head comparison matrices, vendor case studies, third-party pricing directories, and trade/legal commentary. Every claim carries a URL. Anything inferred rather than read is marked `(inf.)`.

**Sourcing warning, read this first.** This category is close to source-free. Almost every number vendors publish is a vendor headline with no baseline, no denominator and no method. Several vendors' own statistics widgets render as literal `0%` or `0x` placeholders on their live pages ([HiJiffy homepage counters](https://www.hijiffy.com/), [Asksuite campaigns page](https://asksuite.com/whatsapp-campaigns/), [Akia homepage](https://akia.com/)), which tells you how much editorial attention those figures get. Hotel Tech Report is the only structured feature matrix in the category and it is a vendor-funded review site. Trust is rated on every benchmark in §4 rather than repeating the marketing.

**Boundaries.** Two sibling agents cover the WhatsApp Business Platform's own capabilities (templates, Flows, carousels, payments, limits, verification) and hotel operations/revenue economics (upsell economics, PMS integration value, review generation, GM metrics). Where this document touches those, it is one sentence and flagged `[sibling turf]`.

---

## 0. The market map

Who actually sells this, at what scale, at what price.

| Product | Positioning | Scale claimed | Published price | HTR standing |
|---|---|---|---|---|
| [Asksuite](https://asksuite.com/) | Reservation-centric AI + contact centre | 5,500+ hotels, 80+ countries, 2.1B messages | Quote only | #1 chatbots, HT 100, ~970 reviews @ 4.9 ([HTR](https://hoteltechreport.com/marketing/hotel-chatbots)) |
| [Canary Technologies](https://www.canarytechnologies.com/products/ai-guest-messaging) | Full guest-management suite, chain-grade | 20,000+ hotels, 125+ countries | Quote only, 3 bundles ([pricing](https://www.canarytechnologies.com/pricing)) | #1 guest messaging HT 100 / 1,534 reviews @ 4.8; #2 chatbots HT 99 ([HTR](https://hoteltechreport.com/guest-experience/guest-messaging-platforms)) |
| [HiJiffy](https://www.hijiffy.com/) | Booking assistant + concierge, EU-centric | 2,600+ hotels, 50+ countries | €99 / €159 / €319 per month + setup ([pricing](https://www.hijiffy.com/plans-and-pricing)) | #3 chatbots HT 98 @ 4.4; #4 guest messaging HT 88 |
| [Duve](https://www.duve.com) | Guest-experience platform, check-in-led | 1,000+ properties, $60M Series B Dec 2025 | $120 / $150 / $200 per month minimums ([pricing](https://www.duve.com/pricing/)) | #2 guest messaging HT 98, 763 reviews @ 4.7 |
| [Akia](https://akia.com/) | Messaging + ops + in-chat "Mini Apps" | 2,000+ customers | Quote only | HT 70 chatbots / 75 guest messaging |
| Quicktext → [Quinta](https://www.quinta.im/features) | Rebranded 2026 (quicktext.im 301-redirects to quinta.im); data distribution + Velma assistant | 38 "native" languages | From €299/month ([Software Advice](https://www.softwareadvice.com/product/484810-Quicktext)) | Listed, no current score |
| [runnr.ai](https://runnr.ai/pricing) | WhatsApp-native, per-unit, incl. hostels/parks | Not stated | €100 / €200 / €400 per month | Top-10 guest messaging, no score |
| [Visito](https://www.visitoai.com/pricing) | Small-property WhatsApp AI with commerce | Not stated | $49 Starter / $399 Pro | HT 78, 40 reviews @ 5.0 |
| [chatlyn](https://chatlyn.com/en/features/whatsapp-for-hotels/) | WhatsApp-first, template/campaign discipline | Not stated | Quote only, Meta costs passed through | HT no score, 5 reviews |
| [D3x](https://www.d3x.ai/pricing) | All-channel AI, EU-hosted, transparent pricing | 60+ European hotel groups | **€5 per room per month**; Phone AI €100/mo + €12/hr | Listed, no score |
| [Whistle for Cloudbeds](https://myfrontdesk.cloudbeds.com/hc/en-us/articles/19512399011355-Whistle-Global-Messaging-SMS-and-WhatsApp-pricing) | PMS-native messaging add-on | Cloudbeds base | Quote; SMS/WhatsApp billed on credits | Category incumbent |
| [Easyway](https://store.apaleo.com/apps/easyway) | WhatsApp check-in into PMS | 100+ languages | Quote only | Apaleo/Mews marketplace |
| [Alliants](https://www.mews.com/en/products/marketplace/alliants-experience-platform) | Luxury concierge + itinerary | 14 channels, 100+ languages | Quote only | Luxury niche |
| [Oaky (Plusgrade)](https://oaky.com/pricing) | Upsell specialist, not messaging | Not stated | Performance-based ("you only pay when we make you money") | Top-tier upselling |
| [Medallia Concierge (ex-Zingle)](https://hoteltechreport.com/compare/medallia-zingle) | Enterprise messaging | Not stated | $179/feature/mo ([Capterra](https://www.capterra.com/compare/161921-181980/Zingle-vs-Whistle)); $300–1,800/mo per location est. ([Spendbase](https://test.spendbase.co/?p=37278)) | 107 reviews @ 4.68 |
| [Book Me Bob](https://www.ttgasia.com/2023/01/31/book-me-bob-ai-chatbot-heads-to-asia-to-improve-customer-service/) | NZ chatbot with its own booking engine | ~80 clients (2023) | Setup fee + monthly by star rating / inventory | Thin footprint |
| [Aara](https://www.mews.com/en/products/marketplace) | WhatsApp concierge in the Mews marketplace | Not stated | Quote only | Marketplace listing |

**Three structural reads from this map.**

1. **The category has split in two.** Canary and Duve sell a *guest-management suite* where messaging is one module beside check-in, keys, upsells, payments and kiosks. Asksuite, HiJiffy and Quinta sell a *reservations assistant* aimed at direct bookings. Harper is neither — it is an in-stay and arrival service bot, which is the smallest slice of the market and the one with the least product built for it.

2. **A WhatsApp-native tier has emerged at Harper's price point.** runnr.ai (€100/mo), Visito ($49/mo), chatlyn and D3x (€5/room/mo) are all newer, WhatsApp-first and priced for an independent. This is the real competitive set for Harper, not Canary. It is also where the feature gap is narrowest and the pricing comparison most unflattering, because these products ship templates, PMS triggers and review requests at €100/month.

3. **Price transparency correlates inversely with size.** The five vendors publishing real numbers (HiJiffy, Duve, runnr, Visito, D3x) are the smaller ones. Canary, Asksuite, Akia, Alliants, Oaky and Medallia are all quote-only — which, per [HotelMinder](https://hotelminder.com/best-hotel-guest-messaging-software), is where setup fees, per-property minimums and premium-integration charges hide.

---

## 1. Feature inventory of the category

The backbone taxonomy below is Hotel Tech Report's own, taken from its head-to-head matrices, because it is the only structured feature list the category has: 13 groups — Unified Inbox, Multi-Channel, Automation, Upselling & Ancillaries, Task & Request Management, Surveys & Feedback, Reporting & Analytics, Compliance & Privacy, Digital Registration & Check-in, Pre-Stay, In-Stay & Post-Stay, Back-Office, Artificial Intelligence ([HTR Akia vs WhatsApp](https://hoteltechreport.com/compare/akia-vs-whatsapp)). The chatbot category adds Bookings & Reservations and Concierge Services ([HTR Asksuite vs HiJiffy](https://hoteltechreport.com/compare/asksuite-hotel-chatbot-vs-hijiffy-hotel-chatbot)).

One calibration before the tables. **HiJiffy's entry tier, at €99/month plus a €99 setup fee, is 25 FAQ topics in 3 languages, on the website only, with a plain link to the booking engine** ([HiJiffy pricing](https://www.hijiffy.com/plans-and-pricing)). Harper's 43 replies in 3 languages, on WhatsApp, with lists, buttons and room cards, is *above* that tier on content and channel. The gap to the market is not the answer library. It is everything that happens around it.

Worth noting too that HTR maintains a profile for **plain WhatsApp as a product**, scored at 0% on all thirteen feature groups with zero verified reviews, and its stated deficiencies are "lacks native automation, guest profiling, or industry-specific tools" and "no verified integrations with hotel-specific PMS or management systems" ([HTR](https://hoteltechreport.com/compare/akia-vs-whatsapp)). Harper is already well past that baseline; the comparison that matters is against the products, not against the channel.

### 1a. Table stakes in 2026

Ships in essentially every serious product. Absence here is a real deficiency.

| # | Feature (concrete) | Who ships it |
|---|---|---|
| T1 | **Unified omnichannel inbox** — web chat, WhatsApp, Instagram, Messenger, email and OTA threads in one staff screen. The concrete spec, from [chatlyn](https://chatlyn.com/en/integrations/whatsapp/): conversation assignment, labels, internal notes with @mentions, snoozing, statuses (open / waiting / snoozed / resolved), the guest's stay shown beside the conversation, a badge showing time left in the 24-hour window that switches the composer to templates when it closes, and the daily messaging limit and quality rating on screen | All. Asksuite Omnichannel CRM, Canary "Unified Inbox", HiJiffy Console (Pro+), Duve Communication Hub (Pro+), Akia, runnr, Visito, chatlyn, Whistle, D3x |
| T2 | **Hotel-scoped FAQ automation** — answers drawn only from hotel-supplied content, escalating rather than guessing outside it | All. [HiJiffy "Aplysia"](https://www.hijiffy.com/our-artificial-intelligence) with anti-hallucination guardrails; [Canary "Responsible AI"](https://www.canarytechnologies.com/products/ai-guest-messaging) citing training, evaluation and real-time monitoring |
| T3 | **Multilingual by auto-detect + machine translation**, 100+ languages, two-way (guest writes native, staff replies native) | Canary "Speak 100+ Languages"; HiJiffy 132 (Pro+), 3 on Basic; Alliants 100+; Easyway 100+; runnr 100+; Quinta 38; Asksuite 50+ |
| T4 | **Human handoff with conversation context** — HTR names "Smooth Handover to Human Agents" as a discrete feature | All |
| T5 | **Approved WhatsApp templates + outbound sends** — build a template, submit to Meta, track approval, send to a segment outside the 24-hour window | chatlyn (template dashboard with Meta approval status, pre-built hotel templates); Asksuite WhatsApp Campaigns; HiJiffy (Premium, "4 campaigns included per reservation"); runnr (Plus tier); Duve Flows; Visito Pro ("WhatsApp Marketing"); Akia; Whistle |
| T6 | **PMS-triggered journey automation** — messages fired on reservation events across booking → pre-arrival → check-in day → in-stay → checkout → post-stay, with a cancellation stopping the remaining sends | chatlyn (5 stay moments, up to 3 timed actions each, cancellation halts the rest); runnr; Duve Flows ("message triggers", "advanced sending conditions"); [Whistle](https://myfrontdesk.cloudbeds.com/hc//articles/8699946508187-whistle-automated-messages-how-to-manage) (arrival/departure/reservation-update/registration triggers, filters, run days and times); Canary; Akia; Quinta |
| T7 | **Live rates and availability in chat, or a date-and-room-prefilled booking deep link** | Asksuite ("Live Inventory Availability", "Room-type Suggestions & Price Check"); [Visito + SiteMinder](https://www.visitoai.com/en/integrations/siteminder) (real-time availability and prices in chat, plus modify/cancel); HiJiffy ("your availability and pricing are always up to date", though the guest "complete[s] the booking directly on the hotel's website") |
| T8 | **Staff-side task/ticket screen** — a request becomes a ticket with a department, an owner and a status, not just a notification | Akia Tasks + Team Chat; Canary auto-generated service tickets pushed to service software; HiJiffy "guest requests and tickets, with assignment per team" (Premium); Duve task management + front-desk dashboard; runnr task-manager integration; [HelloShift](https://www.helloshift.com/ai-assistant) (re-checks open tasks on a per-department clock: guest requests every 10 min, housekeeping every 30) |
| T9 | **Online / pre-arrival check-in with ID capture** — guest detail collection, document or passport scanning, e-signed registration card | Duve (document scanning, e-signed registration card, custom questions, marketing opt-in); [Easyway](https://www.hospitalitynet.org/news/4097359/apaleo-and-easyway-make-it-simple-for-guests-to-check-in-and-communicate-with-hotels-directly-within-whatsapp) (WhatsApp check-in pushing data to Apaleo in real time, own form builder with documents and e-signatures); Akia Digital Check-in (ID + selfie match); Canary Mobile Check-In; HiJiffy (add-on) |
| T10 | **Post-stay review request** routed to Google/TripAdvisor | HiJiffy "Guest reviews campaigns" (internal or external to TripAdvisor/Google); Duve "review optimization"; runnr "review invites"; Visito "WhatsApp review booster" (Pro); Akia Reputation |
| T11 | **Analytics dashboard** — volume, automation/containment rate, CSAT, and an unanswered-question log that shows content gaps | All. HiJiffy's dashboard surfaces "resolved conversations, unanswered questions" specifically to spot content gaps |
| T12 | **Opt-in/consent capture and opt-out** — HTR names "Automated Opt-In/Consent Collection"; chatlyn ships offers as "Opt-in only" | All |
| T13 | **Approved display name + verified Meta business portfolio** — chatlyn states Meta business verification and a Meta business portfolio are *required*, and reads WhatsApp quality rating live; runnr gates "branded WhatsApp number" to its €200 tier | chatlyn (via 360dialog), runnr (Plus+), all enterprise vendors |
| T14 | **Two-way media** — photo sharing in and out, room imagery, document receipt | All (HTR "Photo Sharing") |
| T15 | **Interactive message components** — buttons and lists (chatlyn: templates with up to 2 link buttons; QR concierge menus built from lists of up to ten options with photos) | chatlyn and all WhatsApp-native vendors |

### 1b. Mid-tier

Standard in the upper-mid plans, and routinely the vendor's ROI story.

| # | Feature (concrete) | Who ships it |
|---|---|---|
| M1 | **Pre-arrival upsell with payment capture at the point of offer** | Duve Premium (custom upsells, room-upgrade deals and bids, smart early check-in / late checkout, add-to-hotel-bill, payment-processing connection, third-party supplier connection, pending reservations requiring approval); [Oaky Pre-Stay Upsell](https://oaky.com/en/products/pre-stay-upsell); Canary Dynamic Upsells (listed at 0% commission on its [pricing page](https://www.canarytechnologies.com/pricing)); Akia Upsells; runnr |
| M2 | **In-chat payment / payment link** | Canary Payment Links + Digital Authorizations + Smart Checkout; Duve (stay payment, security deposit, pre-authorisation); Visito Pro commerce at **3% + payment processing**; Akia Card Authorizations; Akia AI Voice takes payment by text link mid-call so card numbers are never spoken |
| M3 | **Charge-to-folio** — post the upsell to the bill with no card re-entry | Duve "add to hotel bill"; HTR names "Charge to Folio". Requires a PMS |
| M4 | **Two-way PMS write-back with auto-approval** — a booked request is approved in the PMS without staff touching it | Oaky ("2-way integration to your PMS… booked requests get approved automatically"); Easyway → Apaleo; Quicktext/Quinta → [SIHOT](https://www.quicktext.im/blog/?p=25534), [Medialog](https://www.quicktext.im/blog/medialog-quicktext-partnership-ai-pms), IDS Next FX Front Desk |
| M5 | **Abandoned-booking and chat recovery** | Asksuite AskFlow Agents, named individually: "Booking Engine Abandonment Agent", "Chat Recovery Agent", "Unavailability Follow-up Agent"; HTR "Booking Recovery Campaigns" |
| M6 | **Native OTA inbox** — Booking.com, Expedia Partner Central and Airbnb answered without logging into the extranet; closing in the tool closes it on Airbnb | [HiJiffy Channels](https://www.hijiffy.com/channels) (Pro+); Duve (Airbnb, Booking.com); runnr; Guestway |
| M7 | **Segmented broadcast campaigns with auto-updating lists** | Asksuite (import leads, up to 1,000 messages at once, smart-tag agent routing); chatlyn (dynamic lists, e.g. "guests arriving within 7 days"); Duve (guest filters and segmentation) |
| M8 | **CSAT and in-stay satisfaction surveys** enabling service recovery before checkout | HiJiffy (satisfaction surveys, CSAT scoring both bot and human agents); Akia Surveys; Duve; HTR "Messaging Guest Surveys" |
| M9 | **Sentiment analysis driving escalation** | HTR AI group (Sentiment Analysis, Self-Learning NLP, Syntax & Semantic Analysis, Behavioral Analysis, Customer Profiling, Prediction & Forecasting); HiJiffy Pro+ |
| M10 | **Digital compendium / guidebook** as a structured in-chat artefact | Canary Digital Compendium; Akia Guidebooks (in-chat "Mini Apps", no download or login); Duve digital spots + branded guest web app |
| M11 | **Canned responses + agent copilot** — a suggested reply the human edits | HiJiffy (the "remaining 10%" routed to staff *with a suggested reply*; Email Copilot drafts from the knowledge base and "nothing goes out without a human check"); Asksuite AI Agent Copilot; Easyway Genie (GPT-4 based, suggests from conversation history); Akia |
| M12 | **Human-in-the-loop controls and audit logs as a configurable product surface** | D3x ("brand voice configuration and human-in-the-loop controls", "full audit logs", EU hosting, MCP server access) |
| M13 | **Multi-property inbox and management** | HiJiffy Pro+; runnr Plus+; Visito Pro (10 businesses); Duve. **Chain/group feature — not a Harper gap** |
| M14 | **Mobile key / keyless entry** | Canary Mobile Keys; Akia Keyless Entry; Alliants; Duve (extra cost). Hardware-dependent |
| M15 | **Voice / phone AI** — AI answers the phone, matches the caller to a reservation, can take payment | [Canary AI Voice](https://www.hospitalitynet.org/news/4130444/canarys-ai-voice-recognized-as-best-hospitality-solution-by-hoteltechreport), named Best Voice & Call Center Software in the 2026 HotelTechAwards; [Akia AI Voice](https://hoteltechreport.com/news/akia-launches-ai-voice-an-ai-receptionist-that-answers-calls-and-books-rooms) (same agent as messaging, now able to speak); D3x Phone AI (€100/mo for 5 hours, then €12/hr) |

### 1c. Premium / enterprise

Mostly irrelevant to a 9-room-type boutique. Listed so they are not mistaken for gaps.

| # | Feature | Who ships it | Relevant to Harper? |
|---|---|---|---|
| P1 | AI agent builder / custom agent studio | Canary AI Agent Studio; Akia "Skills" (staff write a procedure, it becomes a reusable AI skill with Create Task / Dispatch Communication actions) | No — Harper's Worker already *is* this |
| P2 | Group and event lead qualification, quoting, digital contracts | Asksuite Group Quote Agent; Canary Agentic Sales Coordinator + Digital Contracts | No |
| P3 | CRM / loyalty integration and revenue attribution reporting | HiJiffy Pro+ (CRM, sentiment, custom tone of voice); Cendyn and dailypoint via HiJiffy; Revinate | No |
| P4 | SSO/SCIM, governance package, uptime SLA, custom reporting, Power BI | D3x Enterprise; HiJiffy Enterprise (Power BI, custom dashboards, "Powered by" removal) | No |
| P5 | Kiosk and tablet registration | Canary Self-Service Kiosk, Tablet Registration | No |
| P6 | F&B mobile ordering | Canary F&B Mobile Ordering | **No — Harper has no restaurant** |
| P7 | Digital tipping | Canary Digital Tipping; Akia Tipping | Marginal |
| P8 | Collaborative digital itinerary shared across a travel party | Alliants ("collaborate with staff to curate… through their digital itinerary") | No — luxury resort feature |
| P9 | OTA price comparison in chat | HiJiffy; Asksuite "Price Comparison" | **Actively unwanted** — collides directly with Harper's no-price rule |
| P10 | WhatsApp Flows (native forms), carousels, native WhatsApp payments, product catalogues | **Essentially nobody in hospitality ships any of them.** chatlyn is the most WhatsApp-sophisticated vendor in this set — it tracks template approval state, reads the quality rating live and badges the remaining 24-hour window — and **neither of its two WhatsApp pages mentions Flows, carousels, payments or catalogues** ([features](https://chatlyn.com/en/features/whatsapp-for-hotels/), [integration](https://chatlyn.com/en/integrations/whatsapp/)). [360dialog](https://docs.360dialog.com/partner/waba-management/whatsapp-flows) documents WhatsApp payments for India and Singapore only — not Malaysia | **Not a market gap** — see §2c |

---

## 2. Verdict per feature against Harper

Legend: **HAS** · **PARTIAL** · **MISSING** · **N/A** (chain-scale only, not a boutique gap).

### 2a. Table stakes

| # | Feature | Harper | What the gap actually costs a 9-room-type boutique in Sabah |
|---|---|---|---|
| T1 | Unified omnichannel inbox | **MISSING** | The most expensive structural gap after templates. Requests exist as storage rows plus a 1:1 alert to a staff phone, so there is no queue, no owner, no status and no way to tell at 9am what is still open from the night before. One staff phone is also a single point of failure: if that handset is flat or that person is off shift, the request is simply gone. |
| T2 | Hotel-scoped FAQ automation | **HAS** | Harper's is stricter than the market's — see §3.1. |
| T3 | Multilingual, 100+ languages by auto-translation | **PARTIAL** | Three hand-written languages beats HiJiffy Basic's three machine ones on quality, and ML/EN/ZH covers the overwhelming majority of a Sabah property's guests. Real exposure is the fourth language: a Korean or Japanese guest, or an Indonesian writing colloquially, currently gets nothing. Low cost, worth knowing. |
| T4 | Human handoff with context | **PARTIAL** | The handoff exists, but it lands nowhere — there is no inbox for the human to pick up in, so the human picks up in their personal WhatsApp with no transcript view. The guest is answered; the hotel keeps no record and the next shift cannot see it. |
| T5 | **Approved WhatsApp templates + outbound** | **MISSING** | **The single most expensive gap.** Harper can only ever reply inside the 24-hour window, which means it cannot start a conversation — ever. Every proactive feature in this document (T6, T9, T10, M1, M5, M7, M8) is downstream of this one capability. A €100/month competitor has it. [sibling turf: Meta's template mechanics] |
| T6 | PMS-triggered journey automation | **MISSING** | No PMS to trigger from, and no template to send with, so both halves are absent. For Harper the highest-value trigger is trivial and does not need a full PMS: "guest arrives tomorrow" → send arrival instructions. See §6. |
| T7 | Live rates / availability in chat, or prefilled deep link | **PARTIAL** | Harper has a booking link but it is static and carries no dates, no room type and no price. Note the market is weaker here than it sounds: HiJiffy, the #3-ranked chatbot, also makes the guest "complete the booking directly on the hotel's website". The real gap is not in-chat booking — it is availability *awareness* and a prefilled link. Every rate question currently exits WhatsApp cold, which is where direct-booking intent dies. |
| T8 | Staff-side task/ticket screen | **MISSING** | Late check-out, housekeeping, problem reports and airport pickups are exactly the requests that need an owner and a status. Harper raises them as alerts and then loses track of them. On a small team this is survivable day to day and indefensible on a bad day. |
| T9 | Online / pre-arrival check-in with ID capture | **PARTIAL** | ID and payment-slip photos are accepted and forwarded, which is the hard half. What is missing is structure: nothing *asks*, nothing validates that both sides of the IC were sent, nothing files them against a reservation. Staff still re-key everything. |
| T10 | Post-stay review request | **MISSING** | For a boutique with no brand recognition, Google and TripAdvisor volume is the main acquisition asset, and Harper currently has the cheapest possible review channel sitting idle. Needs T5. |
| T11 | Analytics dashboard | **PARTIAL** | Storage rows and logs exist; no dashboard. The real loss is the *unanswered-question log*: Harper cannot see which questions fall through to Claude or to a human, which is the one report that would tell it which reply number 44 should be. |
| T12 | Opt-in / opt-out | **HAS** | STOP/START is shipped. Ahead of several vendors' published behaviour. |
| T13 | Approved display name + verified portfolio | **MISSING** | Two costs. Guests see a raw number rather than "Harper Boutique Hotel", which is precisely the trust signal that makes a stranger's WhatsApp message credible; and the unverified portfolio caps Harper at 250 conversations/day. The cap is almost certainly not binding at current volume `(inf.)`, but the display name is visible to every single guest. [sibling turf: verification mechanics] |
| T14 | Two-way media | **HAS** | Room cards with photos out, ID and payment slips in. |
| T15 | Buttons and lists | **HAS** | Interactive lists and buttons shipped — matches chatlyn's documented set. |

### 2b. Mid-tier

| # | Feature | Harper | What the gap actually costs |
|---|---|---|---|
| M1 | Pre-arrival upsell with payment capture | **MISSING** | Harper already handles late check-out requests manually, which is the single highest-converting upsell in the category. It handles them as a favour instead of as a product. [sibling turf: upsell economics] |
| M2 | In-chat payment / payment link | **MISSING** | Payment slips arrive as photos someone reads by eye. A payment link would remove the reconciliation work and the transcription errors. Note Visito charges 3% + processing for this, so it is not free. |
| M3 | Charge-to-folio | **MISSING** | Needs a PMS. Low priority at this scale. |
| M4 | Two-way PMS write-back with auto-approval | **MISSING** | Needs a PMS. The auto-approval benefit only pays off at a volume Harper does not have `(inf.)`. |
| M5 | Abandoned-booking / chat recovery | **MISSING** | Genuinely valuable and genuinely blocked: it requires both a template (T5) and knowing the guest dropped out (T7). Second-order. |
| M6 | Native OTA inbox | **MISSING** | Real for a Sabah boutique, where Booking.com and Agoda volume is high. Today those conversations live in a separate extranet nobody watches on the same rhythm as WhatsApp. Mid priority. |
| M7 | Segmented broadcast campaigns | **MISSING** | Needs T5. Lower value than it looks for 9 room types — marketing blasts to a small list earn little and risk the WhatsApp quality rating. |
| M8 | CSAT / in-stay surveys | **MISSING** | The cheap version of T10: catching an unhappy guest on day one rather than reading about it on Google on day four. Needs T5. |
| M9 | Sentiment analysis driving escalation | **MISSING** | Harper has a handoff but no trigger for it. A guest writing an angry message in Malay currently gets a canned reply if it pattern-matches. Moderate, and cheap to add. |
| M10 | Digital compendium / guidebook | **PARTIAL** | The 43 replies are the compendium, delivered conversationally. Arguably better than a web app nobody opens. Not a gap. |
| M11 | Canned responses + agent copilot | **PARTIAL** | Harper has the canned library but it serves the *bot*, not the staff member. No suggested-reply surface for a human. |
| M12 | Human-in-the-loop controls + audit logs | **PARTIAL** | The controls are in code rather than in a console, so they are real but not adjustable by staff. For a one-developer property this is the right trade `(inf.)`. |
| M13 | Multi-property | **N/A** | Single property. |
| M14 | Mobile key / keyless entry | **N/A** | Hardware-dependent, and a 4th-floor commercial-building reception is the wrong place to start. |
| M15 | Voice / phone AI | **MISSING, but worth flagging** | Normally a chain feature, except that Canary's own CEO puts unanswered hotel calls at "up to 40 percent", and a property whose reception is on the 4th floor of a commercial building plausibly misses calls at least that often `(inf.)`. D3x prices it at €100/month. Not first, but not dismissible either. |

### 2c. Premium — recorded as not-gaps

P1–P9 are **N/A** for Harper: agent studios, group and event sales, CRM/loyalty, SSO and governance, kiosks, F&B ordering (no restaurant), digital tipping, collaborative itineraries. P9 (OTA price comparison) is **actively unwanted**: it directly contradicts Harper's no-price rule, which §3.2 argues is a strength.

**P10 deserves its own verdict.** Harper lacks WhatsApp Flows, carousels and payments. **This is not a gap against the market.** No hospitality vendor was found shipping all three; chatlyn — the most WhatsApp-disciplined vendor in the set — does not mention Flows, carousels or payments on its WhatsApp-for-hotels page at all; and [360dialog documents WhatsApp payments for India and Singapore only](https://docs.360dialog.com/partner/waba-management/whatsapp-flows), which excludes Malaysia. Building Flows to catch up with the market would be building something the market has not built. The honest framing is that Flows are an *option for Harper's check-in form* (T9), not a competitive deficiency.

---

## 3. What Harper does that the market mostly doesn't

Five of these are real and worth saying out loud. They are not accidents of being small; they are design decisions the market has mostly got wrong.

### 3.1 Approved, word-for-word answers as the default path, with the LLM only as fallback

The entire category sells *grounding and guardrails* as a feature while shipping generative architectures underneath. [HiJiffy's "Aplysia" page](https://www.hijiffy.com/our-artificial-intelligence) states the bot is "not scripted" and finds "verified answers from your approved hotel data", showing a "Verified content" label and a citation to a source PDF — that is retrieval-augmented generation over approved documents, not approved answers. Canary markets "Responsible AI" with "training, evaluation, and real-time monitoring"; D3x markets "human-in-the-loop controls". All are mitigations layered over a generative default.

Harper's default is one step stricter: not generation grounded in approved documents, but **retrieval of an approved string, sent verbatim**, with the model reached only when nothing fits. The difference is that RAG can still paraphrase an approved document into a wrong sentence; a verbatim string cannot.

The evidence that this is the right order comes from the vendors' own worst reviews. HiJiffy's single most negative review theme on Hotel Tech Report is **"Weak Understanding, Robotic Replies, and Conversation Loops" at 100% negative** ([HTR](https://hoteltechreport.com/compare/asksuite-hotel-chatbot-vs-hijiffy-hotel-chatbot)). Akia's is **"Virtual assistant errors" at 100% negative**, described as the chatbot misreading guest questions ([HTR](https://hoteltechreport.com/compare/akia-vs-whatsapp)). On its 43 covered intents, Harper structurally cannot produce either failure.

**The honest caveat:** "robotic" is also a complaint about canned replies, and HiJiffy's reviewers specifically ask for "more natural, personalized interaction". Harper's architecture trades the wrong-answer risk for the stilted-answer risk. That is the better trade in hospitality, but it is a trade, not a free win.

### 3.2 A hard rule that it never states any price

This is the most underrated thing Harper does, and the market does the exact opposite — Asksuite ships "Room-type Suggestions & Price Check", HiJiffy and Asksuite both ship "OTA Price Comparison", Visito shows live rates in chat.

Price and policy answers are precisely where the documented damage is. An independent practitioner review notes that the risk concentrates in "questions where the correct answer is a policy with money attached: cancellation terms, refund eligibility, pet fees, deposits" and gives the failure case of a bot quoting a flexible policy on a non-refundable rate, with "refund demands, chargebacks, or complaints" as the result ([Sagnik Bhattacharya, Sept 2026](https://sagnikbhattacharya.com/blog/hotel-ai-guest-messaging-tools-compared)). And the liability is the hotel's: commentary on hotel chatbots points to the 2024 Air Canada tribunal decision, which rejected the argument that a bot is separate from the business ([Talkory](https://www.talkory.ai/blog/hotel-ai-chatbot-liability-you-own-what-it-says); [Morgan Lewis, Aug 2026](https://www.morganlewis.com/blogs/sourcingatmorganlewis/2026/08/ai-concierge-services-who-is-liable-when-a-bot-books-the-wrong-vacation)).

Harper has eliminated its highest-liability answer class by construction. No vendor advertises this because no vendor can — quoting rates is their direct-booking sales pitch. **Keep this rule.** The right upgrade is not to start quoting prices; it is to hand off price questions faster and with a prefilled link (T7).

### 3.3 Hand-written trilingual replies instead of machine translation of an English master

The market's multilingual story is auto-translation at scale: Canary "100+ Languages", HiJiffy 132, Alliants and Easyway 100+. Nobody publishes per-language quality, and nobody mentions Malay. The available research says the lower-resource pairs are where machine translation degrades, and that hospitality practice is to pair MT with human review ([2025 comparative study on Chinese tourism text](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC12328331/); [Malay MT error analysis](https://hrmars.com/papers_submitted/10540/error-analysis-of-role-play-scripts-translated-from-malay-to-arabic-language-via-google-translate.pdf)).

Harper has done the human review in advance, permanently, for the three languages that actually matter in Kota Kinabalu. That is a quality position no 132-language vendor can match on Bahasa Malaysia, and it is worth saying to guests and to owners. Supporting context: WhatsApp reaches roughly 90–92% of Malaysian internet users ([Statista, 2024](https://de.statista.com/statistik/daten/studie/505966/umfrage/reichweite-von-social-networks-in-malaysia); [Infobip, 2026](https://infobip.com/blog/whatsapp-statistics)), and a trade source describes using WhatsApp to talk to hotels as "completely normal" in Malaysia, Indonesia, Singapore and Hong Kong ([Tageskarte](https://www.tageskarte.io/technologie/detail/whatsapp-wird-zum-zentralen-kommunikationskanal-der-reisebranche.html)).

### 3.4 Published reply-rate limiting and a watchdog sweep

No vendor in this set documents a reply cap or a periodic sweep. Harper's 8-replies-per-10-minutes cap and 5-minute watchdog are operational hygiene the market does not talk about, and they buy three things: they bound the blast radius of exactly the "conversation loops" that are HiJiffy's 100%-negative review theme; they bound cost now that Meta charges for service-window replies `[sibling turf]`; and they protect the WhatsApp quality rating, which chatlyn reads live precisely because it is fragile.

### 3.5 1:1 WhatsApp alerts to a staff phone instead of a staff app

This is listed as a gap in §2 (T8) and it is also, honestly, a strength — and the market offers nothing like it as a first-class mode. Every vendor assumes a staff inbox or app, and the recurring warning is that someone has to be made to watch it: one consultant notes that hoteliers must "define how messaging channels like WhatsApp are used and how their staff should react", and Accor's own WhatsApp programme depends on staff already carrying a mobile operating system the group rolled out first ([Travolution](https://travolution.com/articles/108426/accorhotels-uk-ireland-lets-guests-communicate-with-staff-via-whatsapp)).

Harper's staff need no new app, no new login and no training, and the alert arrives in the one app they already have open. For a reception desk of a few people that is arguably the correct architecture. The fix is not to replace it with a dashboard — it is to add state *behind* it (owner, status, done) while keeping WhatsApp as the delivery surface.

### 3.6 Owning the sender directly — conditional

One real lock-in complaint in this market: "If the vendor registers your WhatsApp number under its own account, leaving can mean losing the number guests already use" ([Sagnik Bhattacharya](https://sagnikbhattacharya.com/blog/hotel-ai-guest-messaging-tools-compared)). Harper runs on the Meta Cloud API through Kapso rather than on a vendor's bundled WABA, which should mean the number and the business portfolio belong to the hotel — **but this depends on whose Meta business portfolio the number sits in, which this research did not verify `(inf.)`. Worth confirming before claiming it.**

---

## 4. Benchmarks

**Trust ratings.** `HIGH` = independent, academic, or a published list price. `MEDIUM` = press, review-site aggregate, or an independent consultancy's range. `LOW-MED` = vendor case study naming a real property. `LOW` = vendor marketing headline with no baseline, no denominator and no method.

**The honest headline: there is no credible independent benchmark for this category.** Not one number below is independent of a vendor's commercial interest except the channel-penetration figures and the consultancy price ranges. Treat the whole section as a map of what vendors *claim* they deliver, which is useful for knowing what to promise and what to measure, and useless as a target.

### 4a. Automation / containment rate

| Figure | Vendor / property | Source | Producer | Date | Sample | Trust |
|---|---|---|---|---|---|---|
| "Automate more than 80% of guest communication" | Canary | [product page](https://www.canarytechnologies.com/products/ai-guest-messaging) | vendor | 2026 | unstated | LOW |
| "more than 80 percent of guest interactions can be handled entirely by AI" | Canary (Harman Singh Narula, CEO) | [Hospitality Net](https://www.hospitalitynet.org/interview/4127995/ai-in-hospitality-canary-technologies-on-voice-messaging-and-revenue-growth) | vendor exec via press | 7 Jul 2025 | industry view, not a measurement | LOW |
| "automated 82% of guest inquiries" | Holiday Inn Express via Canary | [product page](https://www.canarytechnologies.com/products/ai-guest-messaging) | vendor case study | 2026 | 1 property | LOW-MED |
| "up to 90% of guest conversations automatically" | HiJiffy | [homepage](https://www.hijiffy.com/) | vendor | 2026 | unstated | LOW |
| "over 90% of queries independently" *and* "90% of guest queries automatically" — two different figures on one page | HiJiffy Aplysia | [AI page](https://www.hijiffy.com/our-artificial-intelligence) | vendor | 2026 | unstated | LOW |
| 93% | AX Hotels via HiJiffy | [homepage](https://www.hijiffy.com/) | vendor case | 2026 | 1 group | LOW-MED |
| 94% | Entourage sur-le-Lac via HiJiffy | [homepage](https://www.hijiffy.com/) | vendor case | 2026 | 1 property | LOW-MED |
| **100%** | Macdonald Hotels via HiJiffy | [homepage](https://www.hijiffy.com/) | vendor case | 2026 | 1 group | **LOW — a 100% containment rate is not a measurement, it is a tell** |
| "up to 90% of messages" kept from reaching staff | Akia | [homepage](https://akia.com/) | vendor | 2026 | unstated | LOW |
| 86% of guest communication automated | Bellmoor Inn & Spa via Akia | [homepage](https://akia.com/) | vendor case | 2026 | 1 property | LOW-MED |
| "over 80% of outbound messages handled by AI agents" | Rambla via Akia | [homepage](https://akia.com/) | vendor case | 2026 | 1 property | LOW-MED |
| "routine questions that can account for 70-82% of guest messages" | HelloShift | [AI assistant page](https://www.helloshift.com/ai-assistant) | vendor | 2026 | unstated | LOW |

**Honest range.** Vendors converge on a claimed 80–90%, and nobody publishes a definition. "Automated" could mean conversations with zero human touch, or individual messages, or resolved intents — three numbers that differ by a factor of several. Macdonald Hotels at 100% settles the question of whether these are measured consistently. **For Harper:** the only meaningful containment figure is Harper's own, measured against its own fall-through log (gap #9). Do not adopt 80% as a target inherited from marketing.

### 4b. Deflection of calls and emails

| Figure | Vendor / property | Source | Producer | Date | Sample | Trust |
|---|---|---|---|---|---|---|
| 70% call reduction | Lake District Hotels via HiJiffy | [homepage](https://www.hijiffy.com/) | vendor case | 2026 | 1 group | LOW-MED |
| "up to 40 percent of calls to hotels go unanswered" | Canary CEO | [Hospitality Net](https://www.hospitalitynet.org/interview/4127995/ai-in-hospitality-canary-technologies-on-voice-messaging-and-revenue-growth) | vendor exec via press | 7 Jul 2025 | unstated | LOW-MED — a problem statement, not a result, but the most quoted number in the category |
| ~7 hours/week saved on pre-arrival communication | one property via Whistle | [Hospitality Tech](https://hospitalitytech.com/introducing-whistle-cloudbeds-new-guest-engagement-solution-powered-cloudbeds) | vendor via press | 2022 | 1 property | LOW-MED |
| 25% of the workday saved | Winter Park via Akia | [homepage](https://akia.com/) | vendor case | 2026 | 1 property | LOW-MED |
| "30% fewer" staff workload | HelloShift | [press item](https://www.helloshift.com/news/automate-hotel-guest-texts-with-helloshift-ai-to-cut-staff-workload-30) | vendor | 2026 | unstated | LOW |
| 30–40% fewer front-desk calls | ChatDaddy (generic WhatsApp vendor, not hotel-specific) | [blog](https://chatdaddy.tech/blog/whatsapp-for-hotels) | vendor | 2026 | unstated | LOW |

### 4c. Response time

| Figure | Property | Source | Trust |
|---|---|---|---|
| First response 10 minutes → under 1 minute | The LINE SF via Canary | [product page](https://www.canarytechnologies.com/products/ai-guest-messaging) | LOW-MED |

Only one published before/after figure was found in the entire category. **For Harper** this is the one benchmark that is trivially already beaten: a canned reply from a Worker is sub-second.

### 4d. Direct-booking conversion from chat

| Figure | Vendor | Source | Trust |
|---|---|---|---|
| "23x average ROI" | Asksuite | [homepage](https://asksuite.com/) | LOW — ROI undefined, no baseline, no cost side |
| 7.9x ROI | Lub d via HiJiffy | [homepage](https://www.hijiffy.com/) | LOW-MED |
| "booking conversion" counter | HiJiffy homepage | [homepage](https://www.hijiffy.com/) | **renders as 0% — a broken placeholder** |
| ~$200K in bookings via chatbot | Turtle Bay Resort via Book Me Bob | [case study listing](https://www.casestudies.com/company/hoteltechreport/case-study/turtle-bay-resort-delivers-200k-in-bookings-via-its-ai-chatbot-from-book-me-bob) | LOW-MED — title only; figures not retrievable |

**No credible published chat-to-booking conversion rate exists.** And the one independent observation about the measurement is damning: Asksuite's booking counts "may double-count or miss bookings made after a chat, so they should be checked against the booking engine's own report" ([Sagnik Bhattacharya, 27 Sept 2026](https://sagnikbhattacharya.com/blog/hotel-ai-guest-messaging-tools-compared), MEDIUM). That is the single most useful line in this section: the category's headline revenue claims rest on attribution nobody has audited.

### 4e. Review-score movement

**No credible published figure was found, from any vendor or any independent source.** Vendors sell review *requests* (HiJiffy, Duve, runnr, Visito, Akia) and none of them publishes a measured score delta or review-volume lift. If a vendor claims one in a sales call, ask for the method. `[sibling turf: review generation economics]`

### 4f. Adoption and engagement rates

| Figure | Vendor / property | Source | Date | Trust |
|---|---|---|---|---|
| **~90–92% of Malaysian internet users use WhatsApp monthly** | n/a — channel data | [Statista](https://de.statista.com/statistik/daten/studie/505966/umfrage/reichweite-von-social-networks-in-malaysia) (2024, 92%); [Infobip](https://infobip.com/blog/whatsapp-statistics) (2026, ~90%) | 2024–26 | **MEDIUM-HIGH — the only solid number in this section, and it validates Harper's channel choice** |
| Using WhatsApp to talk to hotels is "completely normal" in Malaysia, Indonesia, Singapore, Hong Kong | industry source | [Tageskarte](https://www.tageskarte.io/technologie/detail/whatsapp-wird-zum-zentralen-kommunikationskanal-der-reisebranche.html) | 2026 | MEDIUM |
| 60% online check-in completion | Kora Living via HiJiffy | [homepage](https://www.hijiffy.com/) | 2026 | LOW-MED |
| 35.1% "average guest usage rate" | Easyway via Mews | [Mews blog](https://www.mews.com/en/blog/communicate-with-your-guests-via-their-favourite-messaging-app-with-easyway) | 2020 — **six years old** | LOW |
| WhatsApp campaign open rates "above 80%" | HiJiffy | [homepage](https://www.hijiffy.com/) | 2026 | LOW |
| ~95% open rates | chatlyn | [WhatsApp newsletter page](https://chatlyn.com/en/features/whatsapp-newsletter/) | 2026 | LOW |
| WhatsApp open rates "up to 3x higher than email" | Asksuite | [campaigns page](https://asksuite.com/whatsapp-campaigns/) | 2026 | LOW — and the page's own stat widgets render as 0% |

### 4g. Upsell conversion and incremental revenue

| Figure | Vendor / property | Source | Trust |
|---|---|---|---|
| **€5–15 per occupied room per month** | n/a — consultancy range | [HotelMinder](https://hotelminder.com/best-hotel-guest-messaging-software) | **MEDIUM — the most credible number here, because it is a range from a non-vendor** |
| $180 per room per month uplift | Duve | [duve.com](https://www.duve.com) | LOW |
| "up to €50 extra revenue per room per month" | runnr | [upsell page](https://runnr.ai/solutions/automatic-upsell) | LOW |
| **€65 per room per month** | 200-room **Jakarta** hotel via runnr | [runnr](https://runnr.ai/pricing) | LOW-MED — **the closest geographic analogue to Harper in this entire teardown** |
| £43 per room per month | 70-room London property via runnr | [runnr](https://runnr.ai/pricing) | LOW-MED |
| "Boost upsell revenue by 4x" | Canary | [product page](https://www.canarytechnologies.com/products/ai-guest-messaging) | LOW — **the page states no baseline** |
| "65% of early check-in revenue through AI upsells" | The LINE SF via Canary | [product page](https://www.canarytechnologies.com/products/ai-guest-messaging) | LOW-MED |
| $1,700 incremental monthly revenue | Holiday Inn Express via Canary | [product page](https://www.canarytechnologies.com/products/ai-guest-messaging) | LOW-MED |
| TRevPAR "up to 5%" | Oaky | [pre-stay upsell](https://oaky.com/en/products/pre-stay-upsell) | LOW — no method, period or property set |
| 10.8% deal conversion rate | Oaky | third-party listings via [Mews marketplace](https://www.mews.com/products/marketplace/oaky) | LOW-MED |
| "up to €250 extra spend per guest" | Oaky | third-party listings | LOW |
| $89K / $75K / $13K post-stay revenue | Akia case studies | [homepage](https://akia.com/) | LOW-MED |
| Guest spend boost "up to 46%" | Easyway via Mews | [Mews blog](https://www.mews.com/en/blog/communicate-with-your-guests-via-their-favourite-messaging-app-with-easyway) | LOW — 2020 |
| 25% higher upsell conversion | ChatDaddy (generic) | [blog](https://chatdaddy.tech/blog/whatsapp-for-hotels) | LOW |

**Honest range for a boutique.** The non-vendor range (€5–15 per occupied room per month) and the nearest real comparable (€65/room/month at a 200-room Jakarta hotel) differ by roughly 4–13x, which is the measure of how little anyone knows. `[sibling turf: upsell economics]`

### 4h. Pricing — the best-sourced part of this teardown

| Model | Figure | Source | Trust |
|---|---|---|---|
| Per room, published | **€5 / room / month** (all channels; Phone AI +€100/mo for 5 hrs, then €12/hr) | [D3x](https://www.d3x.ai/pricing) | HIGH (list price) |
| Per room, SMS-only platforms | €1–2 / room / month | [HotelMinder](https://hotelminder.com/best-hotel-guest-messaging-software) | MEDIUM |
| Per room, full-featured | **€3–8 / room / month** | [HotelMinder](https://hotelminder.com/best-hotel-guest-messaging-software) | MEDIUM |
| Per room, generic guides | $1–4 and $2–15 / room / month | third-party guides | LOW-MED |
| Flat monthly | €50–300 / month typical | [HotelMinder](https://hotelminder.com/best-hotel-guest-messaging-software) | MEDIUM |
| Flat monthly | $50–100 basic; $200–500 comprehensive | [Visito guide](https://www.visitoai.com/blog/best-guest-messaging-solutions-and-software) | LOW (vendor) |
| Tiered, published | HiJiffy €99 / €159 / €319 per month + **€99 / €399 / €599 setup** | [HiJiffy](https://www.hijiffy.com/plans-and-pricing) | HIGH |
| Tiered, published | Duve $120 / $150 / $200 per month minimums; **SMS & WhatsApp messaging is an extra charge even on Pro** | [Duve](https://www.duve.com/pricing/) | HIGH |
| Tiered, published | runnr €100 / €200 / €400 per month; 12-month agreement with a first-month trial; no setup fee | [runnr](https://runnr.ai/pricing) | HIGH |
| Tiered, published | Visito $49 Starter / $399 Pro — **but the page's own FAQ quotes $1,499/month for the top credit tier, contradicting the grid** | [Visito](https://www.visitoai.com/pricing) | HIGH with a flagged internal contradiction |
| Tiered | Quinta (ex-Quicktext) from €299 / month | [Software Advice](https://www.softwareadvice.com/product/484810-Quicktext) | MEDIUM |
| Per feature | Medallia Concierge $179 / feature / month | [Capterra](https://www.capterra.com/compare/161921-181980/Zingle-vs-Whistle) | MEDIUM |
| Per location, estimated | Medallia $300–500/mo entry; $1,000–1,800/mo large property | [Spendbase](https://test.spendbase.co/?p=37278) | LOW (aggregator's internal data) |
| Commission | Visito commerce agent fee **3% + payment processing** | [Visito](https://www.visitoai.com/pricing) | HIGH |
| Commission | Canary Dynamic Upsells listed at **0% commission** | [Canary](https://www.canarytechnologies.com/pricing) | MEDIUM |
| Performance | Oaky: "you only pay when we make you money", monthly price based on performance and property size | [Oaky](https://oaky.com/pricing) | MEDIUM |
| Quote-only | Canary, Asksuite, Akia, Alliants, Whistle, Easyway, Book Me Bob | vendor pages | — |
| Meta pass-through | runnr: "approximately €0.75 per room per month" on average | [runnr](https://runnr.ai/pricing) | LOW-MED (vendor average, varies by guest country and message category) |
| Meta pass-through | chatlyn passes Meta cost through "with its service charge"; Whistle bills SMS/WhatsApp on **credits**, varying by country | [chatlyn](https://chatlyn.com/en/features/whatsapp-for-hotels/), [Cloudbeds](https://myfrontdesk.cloudbeds.com/hc/en-us/articles/19512399011355-Whistle-Global-Messaging-SMS-and-WhatsApp-pricing) | MEDIUM |
| Meta's own agent | ~4–5 cents per message, token-billed | [Sagnik Bhattacharya](https://sagnikbhattacharya.com/blog/hotel-ai-guest-messaging-tools-compared) | MEDIUM |

**One sentence on the platform change, flagged as sibling turf.** From 1 October 2026 Meta charges for replies sent inside the 24-hour service window, with 1,000 free replies per business number per month ([Sagnik Bhattacharya](https://sagnikbhattacharya.com/blog/hotel-ai-guest-messaging-tools-compared), MEDIUM) — relevant here only because it means Harper's 8-per-10-minute reply cap is now a cost control as well as a safety one. `[sibling turf]`

**What Harper should expect.** Buying the category at boutique scale costs €100–320/month flat, or €3–8 per room per month, plus Meta pass-through, plus setup fees of €99–599 where published. Harper's current marginal cost is a Worker, Kapso and Meta conversations, which is almost certainly below the floor of that range `(inf.)`. **The pricing comparison therefore favours Harper, and the strategic question is not whether to buy but which €100/month features are worth building.**

---

## 5. The critical reviews — the best map of what not to build

Hotel Tech Report publishes per-theme sentiment percentages on its head-to-head pages. Those percentages are the most useful artefact in this teardown, because they are derived from hoteliers who already paid.

### 5a. What hoteliers complain about after buying

**Theme 1 — PMS and integration depth is the category's single biggest complaint, and it hits the leaders hardest.** Recurs across the two top-ranked guest-messaging platforms.

- **Duve: "PMS and system integration" — 71% NEGATIVE.** Its worst theme, on the #2-ranked platform in the category ([HTR](https://hoteltechreport.com/compare/duve-upselling-vs-upselling-hotel)).
- **Canary:** HTR's own review summary names "PMS integrations" as "weaker than the rest of the product" ([HTR](https://hoteltechreport.com/guest-experience/guest-messaging-platforms/canary-technologies), 1,912 reviews @ 4.8).
- Independent commentary warns that PMS messaging "may offer templates rather than AI replies", and that Meta's own Business Agent "cannot see reservations, so it answers only from general property information" ([Sagnik Bhattacharya](https://sagnikbhattacharya.com/blog/hotel-ai-guest-messaging-tools-compared)).
- HotelMinder advises confirming "your specific PMS is supported before buying" and calls PMS integration "non-negotiable" in the same breath — a contradiction that tells you how often it disappoints.

> **What this means for Harper.** The market's most-complained-about feature is the one Harper lacks. That is not an argument for skipping it; it is an argument against building it deeply. A read-only "who arrives tomorrow" feed captures most of the value that hoteliers are disappointed by, at a fraction of the work.

**Theme 2 — the bot misunderstands, loops, or sounds robotic.** The most consistent complaint across every product.

- **HiJiffy: "Weak Understanding, Robotic Replies, and Conversation Loops" — 100% NEGATIVE** ([HTR](https://hoteltechreport.com/compare/asksuite-hotel-chatbot-vs-hijiffy-hotel-chatbot)). Separately, "Chatbot Tone and Interaction Challenges" — 100% negative, with reviewers finding it "robotic" and wanting "more natural, personalized interaction" ([HTR](https://hoteltechreport.com/compare/hijiffy-vs-whatsapp)).
- **Akia: "Virtual assistant errors" — 100% NEGATIVE**, described as the chatbot "sometimes misreads guest questions" ([HTR](https://hoteltechreport.com/compare/akia-vs-whatsapp)).

> **For Harper:** both halves of this complaint are live, and Harper has chosen a side. Verbatim strings immunise it against *misreading and looping*; they expose it to *sounding canned*. That is the right trade in hospitality, but the mitigation is writing warmer strings, not adding generation.

**Theme 3 — technical glitches and reliability.** Recurrent, and the oldest product in the set is worst.

- **Medallia Concierge / Zingle: "Technical glitches" — 96% NEGATIVE** ([HTR](https://hoteltechreport.com/compare/chatlyn-vs-medallia-zingle)).
- **Canary:** "form and notification glitches" named in HTR's review summary.

> **For Harper:** the 5-minute watchdog is answering a complaint the market demonstrably has. Keep it and say so.

**Theme 4 — customisation inflexibility.** Recurs across three products.

- **Medallia: "Customization" — 58% negative** ([HTR](https://hoteltechreport.com/compare/chatlyn-vs-medallia-zingle)).
- **Asksuite: "Customization Flexibility" — 45% negative** ([HTR](https://hoteltechreport.com/compare/asksuite-hotel-chatbot-vs-hijiffy-hotel-chatbot)).
- **HiJiffy:** "Customization and Flexibility" listed as a con; reviewers want more control over messaging tone and dashboards. Also flagged in a separate HTR comparison as "limited customization and occasional setup complexity".

> **For Harper:** this is the structural advantage of owning the Worker. Everything is custom by construction. Do not trade it for a vendor console.

**Theme 5 — reporting and attribution nobody believes.**

- **Asksuite: "Reporting and Analytics" — 69% NEGATIVE**, on the #1-ranked chatbot in the category ([HTR](https://hoteltechreport.com/compare/asksuite-hotel-chatbot-vs-hijiffy-hotel-chatbot)).
- The specific failure: Asksuite's booking counts "may double-count or miss bookings made after a chat" ([Sagnik Bhattacharya](https://sagnikbhattacharya.com/blog/hotel-ai-guest-messaging-tools-compared)).
- HiJiffy fares better here — "Reporting, Tracking, and Analytics Visibility" 73% *positive* — so this is product-specific rather than universal.

> **For Harper:** build the unanswered-question log, not an attributed-revenue dashboard. The expensive half of analytics is the half hoteliers distrust.

**Theme 6 — support responsiveness and self-service.**

- **HiJiffy: "Support Responsiveness and Self-Service Limitations" — 87% NEGATIVE** ([HTR](https://hoteltechreport.com/compare/asksuite-hotel-chatbot-vs-hijiffy-hotel-chatbot)). Notable given HiJiffy sells "dedicated support" and an account manager at Pro and Premium.

**Theme 7 — guest-facing friction in verification and payment flows.** Directly relevant to Harper's check-in ambitions.

- **Canary:** "Some guests find the verification and authorization flows cumbersome" (HTR review summary).
- **Akia: "Credit card authorization" — 44% negative**, with users relying on third-party tools for card processing ([HTR](https://hoteltechreport.com/compare/akia-vs-whatsapp)).
- **Duve: "Guest app and branded guest journey" — 47% negative** ([HTR](https://hoteltechreport.com/compare/duve-upselling-vs-upselling-hotel)).

> **For Harper:** this is why structured online check-in sits at #7 rather than #3. Harper's current "send me a photo of your IC" may well convert better than a form, and the branded guest app that Duve customers complain about is a thing Harper has wisely never built.

**Theme 8 — hidden costs and pricing opacity.**

- "Headline prices differ less than they look", because "setup fees, per-property minimums and WhatsApp's own message charges sit outside them" ([Sagnik Bhattacharya](https://sagnikbhattacharya.com/blog/hotel-ai-guest-messaging-tools-compared)).
- Specific gates: HiJiffy includes WhatsApp only on Premium and caps Basic at 3 languages; Duve's AI may be extra; **Canary's AI replies start only at the Advanced tier** — so a cheap Canary quote contains no AI at all.
- HotelMinder: watch for setup fees, per-message charges above a volume threshold, premium integrations and long-term contracts.
- runnr commits you to a 12-month agreement.

**Theme 9 — WhatsApp number lock-in.** Single-source but serious.

- "If the vendor registers your WhatsApp number under its own account, leaving can mean losing the number guests already use" ([Sagnik Bhattacharya](https://sagnikbhattacharya.com/blog/hotel-ai-guest-messaging-tools-compared)).

**Theme 10 — confidently wrong answers where being wrong costs money or health.** The most consequential theme, and the one Harper has already designed around.

- The archetype: a tool told a guest with coeliac disease that breakfast would be fine, "which nobody had verified" ([Sagnik Bhattacharya](https://sagnikbhattacharya.com/blog/hotel-ai-guest-messaging-tools-compared)).
- Risk concentrates in "questions where the correct answer is a policy with money attached: cancellation terms, refund eligibility, pet fees, deposits, accessibility features" ([Talkory](https://www.talkory.ai/blog/hotel-ai-chatbot-liability-you-own-what-it-says)).
- Liability sits with the hotel: commentary points to the 2024 Air Canada tribunal decision rejecting the argument that a bot is separate from the business ([Talkory](https://www.talkory.ai/blog/hotel-ai-chatbot-liability-you-own-what-it-says); [Morgan Lewis, Aug 2026](https://www.morganlewis.com/blogs/sourcingatmorganlewis/2026/08/ai-concierge-services-who-is-liable-when-a-bot-books-the-wrong-vacation)).
- Operationally: urgent issues such as alarms or no hot water "need an alert to on-call staff, not a queued reply" ([Sagnik Bhattacharya](https://sagnikbhattacharya.com/blog/hotel-ai-guest-messaging-tools-compared)) — which is precisely what Harper's 1:1 WhatsApp alert already does, and what an inbox-based competitor does not.

**Theme 11 — geographic coverage, which matters disproportionately for Sabah.**

- HiJiffy's visible integration directory is Europe- and LatAm-centric (Apaleo, Cloudbeds, D-EDGE, Dingus, Desbravador, e-GDS, Civitfun, Bowo, Cendyn, dailypoint); **no Southeast Asian systems appear among the names shown**, though the list is truncated behind a "Load more" button, and the page's own integration count is internally inconsistent (100+ in the header, 122 in the section, 60+ in the FAQ) ([HiJiffy](https://www.hijiffy.com/integrations)).
- Among Malaysian and regional PMS options, only Hotelogix has a described WhatsApp path, via [Gupshup](https://www.hotelogix.com/marketplace/product/gupshup); [Softinn](https://www.mysoftinn.com), a Malaysian vendor, has no chatbot and only a click-to-WhatsApp link in the guest folio; eZee's Malaysia material covers tax and MyKad features with no WhatsApp or chatbot.

> **For Harper this is the strongest single argument against buying.** A vendor Harper might purchase would plausibly not integrate with Harper's PMS or booking engine anyway, which means Harper would be paying €100–320/month for templates, an inbox and a dashboard — and building the integration itself regardless.

### 5b. What guests complain about

**State of the evidence, honestly:** far less guest-side than hotelier-side material exists, and **no independent survey of hotel guests' channel or bot preferences in Southeast Asia was found.** Web-search budget was exhausted before this could be pushed further; it is the clearest hole in this teardown. What the available sources support:

| Complaint | Evidence | Source |
|---|---|---|
| Verification and authorization flows are cumbersome | Named in HTR's review summary for Canary, reported as guest friction | [HTR](https://hoteltechreport.com/guest-experience/guest-messaging-platforms/canary-technologies) |
| Guests blame the property for the bot's errors | Hallucinated "amenity, policy, and pricing claims that guests attribute to properties, causing refunds, one-star reviews, and legal exposure" | [Talkory](https://www.talkory.ai/blog/hotel-ai-chatbot-liability-you-own-what-it-says) |
| Guests treat the bot as the business | "customers, and tribunals, tend to treat your chatbot as you" | [Talkory](https://www.talkory.ai/blog/hotel-ai-chatbot-liability-you-own-what-it-says) |
| Bot answers on health and dietary matters are trusted and should not be | The coeliac breakfast case | [Sagnik Bhattacharya](https://sagnikbhattacharya.com/blog/hotel-ai-guest-messaging-tools-compared) |
| Bot sounds robotic and loops | Hoteliers reporting guest-facing behaviour, HiJiffy 100% negative | [HTR](https://hoteltechreport.com/compare/hijiffy-vs-whatsapp) |

**What the guest-side complaints say about what not to build, for Harper specifically.**

1. **Do not put a form between a guest and a human.** Verification friction is the one complaint that is unambiguously guest-side across two products.
2. **Do not let the bot answer anything where being wrong costs money or health.** Harper's no-price rule already covers the money half. The health half — allergies, dietary, accessibility, medical — deserves the same hard rule, and a property with no restaurant has an easy answer available: hand off.
3. **Do not queue urgent messages.** Harper's 1:1 alert is the correct design and is better than an inbox for this case.
4. **Warmth, not generation, is the fix for "robotic".** The complaint is about tone, and tone is editable in 43 strings.

---

## 6. Priority synthesis

### 6a. The top 10 gaps against Harper, in priority order

Ordered by value to *this* property, net of what it costs to build, and net of whether the market's own customers complain about the feature after buying it.

| # | Gap | Why here | Blocked by |
|---|---|---|---|
| 1 | **No approved message template** | Harper cannot start a conversation. Every proactive capability in the category is downstream of this one thing. A €100/month competitor ships it. | Meta template approval |
| 2 | **Unverified business portfolio / no approved display name** | Same workstream as #1 and partly a prerequisite for trust: every guest sees a raw number instead of the hotel's name. Also lifts the 250/day cap. | Meta business verification |
| 3 | **No pre-arrival sequence** | The highest-value single message this property could send: arrival time, and how to find a reception on the 4th floor of a commercial building. That is Harper's most confusing physical fact and it is currently explained only reactively. | #1, #2 |
| 4 | **No rates/availability awareness and no prefilled booking link** | Every rate question exits WhatsApp cold. Note the market is weaker here than it markets — HiJiffy also sends the guest to the website — so the target is availability awareness plus a dates-and-room-prefilled link, not in-chat booking. | A read-only feed from the booking engine |
| 5 | **No staff-side state behind the alerts** | Requests have no owner, no status and no morning-after view. Keep WhatsApp as the delivery surface; add state behind it. | Nothing |
| 6 | **No post-stay review request** | A boutique with no brand recognition lives on Google and TripAdvisor volume, and the cheapest possible review channel is sitting idle. | #1 |
| 7 | **No structured online check-in / ID capture** | Harper already accepts ID photos, which is the hard half. The missing half is asking, validating and filing. Deliberately below #6 because guest friction in verification flows is a *named complaint* against Canary and Akia. | #1 for the prompt |
| 8 | **No upsell with payment** | Late check-out is already Harper's most-handled request and the category's best-converting offer, handled today as a favour rather than a product. | #1, a payment link |
| 9 | **No analytics, specifically no unanswered-question log** | Harper cannot see which questions fall through, which is the one report that tells it what reply 44 should be. Note attributed-revenue dashboards are the market's most-complained-about feature, so build the cheap half only. | Nothing |
| 10 | **No OTA inbox, no abandoned-booking recovery** | Real for a Sabah property with heavy Booking.com and Agoda volume, but second-order and the most work for the least certain return. | #1, OTA API access |

**Explicitly not gaps.** WhatsApp Flows, carousels and native payments (the market has not built them either, and WhatsApp payments are not available in Malaysia); multi-property management; mobile keys; kiosks and tablet registration; F&B mobile ordering (no restaurant); group and event sales; CRM/loyalty and revenue attribution; SSO and governance; collaborative itineraries. **Actively unwanted:** in-chat OTA price comparison, which contradicts the no-price rule.

**One wildcard.** Voice/phone AI is normally a chain feature, but Canary's co-founder and CEO puts unanswered hotel calls at "up to 40 percent" ([Hospitality Net, 7 Jul 2025](https://www.hospitalitynet.org/interview/4127995/ai-in-hospitality-canary-technologies-on-voice-messaging-and-revenue-growth)), and a 4th-floor reception plausibly misses calls at least that often `(inf.)`. D3x prices it at €100/month for five hours. Not top-10, but worth a deliberate decision rather than an omission.

### 6b. The three things Harper already does better than the market

1. **It never states a price.** The category does the opposite and sells it as a feature, and price-and-policy answers are exactly where the documented damage lands — refund demands, chargebacks, one-star reviews, and a 2024 tribunal precedent holding the business responsible for what its bot said. Harper has deleted its highest-liability answer class by construction. Keep the rule; make the handoff on price faster instead.

2. **It sends approved strings verbatim rather than generating from approved documents.** The market's grounding story is RAG with a "verified content" label, and RAG can still paraphrase a correct document into a wrong sentence. The two most negative review themes in the entire category are HiJiffy's "Weak Understanding, Robotic Replies, and Conversation Loops" (100% negative) and Akia's "Virtual assistant errors" (100% negative). On its 43 covered intents Harper cannot produce those.

3. **Three hand-written languages beat 132 machine-translated ones for Kota Kinabalu.** Malay, English and Chinese, written once by a human, in a market where WhatsApp reaches roughly 90–92% of internet users. No vendor publishes Malay quality; the research says lower-resource pairs are where machine translation degrades. HiJiffy charges €99/month for three machine-translated languages — Harper matches that language count with better text.

Two honourable mentions worth keeping and saying out loud: the **reply cap and watchdog**, which no vendor documents and which bound exactly the loop failure the market complains about; and **1:1 WhatsApp alerts with no staff app**, which is the one architecture that gets actually used by a reception team of a few people, and which the market offers nowhere as a first-class mode.

### 6c. The single feature to add first

**An approved WhatsApp template, plus the Meta business verification needed to use it — delivered as one pre-arrival message the day before check-in.**

Everything else in the top 10 is gated by it. Pre-arrival instructions, review requests, upsell offers, check-in prompts, CSAT, abandoned-booking recovery and every PMS-triggered journey in the category are all the same unlock: the ability to speak first. Every product in this teardown for which template support could be confirmed has it — chatlyn, Asksuite, HiJiffy (Premium), runnr (Plus), Duve, Visito (Pro), Akia and Whistle. Harper does not.

It is also the cheapest item on the list and the one that fits Harper's existing architecture without changing it: one utility template, one trigger, one new string in three languages. And the content is already decided by the property's own geography — *your stay is tomorrow, reception is on the 4th floor, here is how to get in, what time will you arrive?* That single message answers Harper's most confusing physical fact proactively instead of reactively, opens a 24-hour window in which the existing 43 replies can do their work, and collects the one piece of data (arrival time) that staff currently have to chase.

Build the template before the dashboard, the PMS integration, or the Flow.

---

## Appendix: research limitations

Stated plainly so nothing here is trusted more than it deserves.

**What could not be verified.**

- **No independent benchmark exists for this category.** Every automation, deflection, conversion and upsell figure in §4 traces to a vendor. The only exceptions are the WhatsApp channel-penetration figures (Statista, Infobip) and HotelMinder's price and upsell ranges. No academic or large-sample study of hotel chatbot containment was found.
- **No measured review-score movement** was found from any source, vendor or independent (§4e).
- **No published chat-to-direct-booking conversion rate** was found, and the one independent comment on the measurement says the vendor's own counts may be wrong (§4d).
- **No independent survey of hotel guests' channel or bot preferences in Southeast Asia** was found. §5b is consequently thinner than §5a, and that asymmetry reflects the available evidence, not a judgement that guests complain less.
- **No measured accuracy figure for any hotel chatbot in Bahasa Malaysia or Chinese** exists publicly. §3.3's argument rests on general machine-translation research about lower-resource language pairs, not on a hospitality-specific measurement. It is a well-founded inference, not a proven claim.
- **Harper's WhatsApp sender ownership** (whose Meta business portfolio the number sits in) was not verified — see §3.6, marked `(inf.)`.
- **Harper's actual room count** is unknown; only "9 room types" was given. Per-room pricing comparisons in §4h are therefore expressed as rates, not totals.

**Method caveats.**

- **Hotel Tech Report is the backbone of §1, §2 and §5, and it is a vendor-funded review site.** Its sentiment percentages are derived from reviews solicited by vendors. They are the best structured data available and they are not neutral. Its own pages are internally inconsistent in places: review counts and ratings for the same product differ between pages (Akia appears as 4.8, 4.84, 4.9 and 4.93 across one page), and per-feature checkmarks do not survive page extraction, so §1's matrices are group-level.
- **Several vendor pages publish broken statistics.** HiJiffy's homepage counters, Asksuite's campaign-page widgets and Akia's homepage stats render as `0%` or `0x`. Figures from those pages were taken from body copy and case studies, not the widgets.
- **Vendor page inconsistencies were recorded rather than resolved** where they matter: HiJiffy's integration count (100+ / 122 / 60+), Asksuite's review count (970 / "nearly 1,000" / 900+) and award claims (6 years / 7th consecutive year), and Visito's Pro price ($399 in the grid vs $1,499 in the FAQ).
- **Several targets returned HTTP 404** and were worked around via search or alternative URLs: hijiffy.com/features, asksuite.com/features, canarytechnologies.com/products/dynamic-upsells, oaky.com/how-it-works, the SiteMinder chatbot plug-in help article, and several Hotel Tech Report comparison slugs including every attempted Canary head-to-head.
- **Quicktext has rebranded to Quinta** (quicktext.im 301-redirects to quinta.im) and its feature pages now describe data distribution more than messaging, so Velma's current messaging capabilities are less documented than its PMS partnership press releases suggest.
- **Web-search budget was exhausted** before guest-side evidence (§5b) and Canary's per-theme negative percentages could be pushed further. Those two are the highest-value follow-ups if this is revisited.

**Deliberate scope exclusions.** WhatsApp Business Platform mechanics (template categories, Flows, carousels, payments, rate limits, verification tiers) and hotel operations and revenue economics (upsell ROI modelling, PMS integration value, review-generation mechanics, GM-level metrics) belong to the two sibling research tracks and are touched here only where a competitive claim required it — each such place is marked `[sibling turf]`.
