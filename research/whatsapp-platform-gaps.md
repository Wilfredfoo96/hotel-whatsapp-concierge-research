# WhatsApp Business Platform — Capability Audit & Gap Analysis for Harper

**Subject:** Harper hotel concierge, one WhatsApp Business number `the hotel WhatsApp number`, Cloud API via Kapso, boutique hotel in Sabah, Malaysia (ms / en / zh).
**Date of audit:** 2026-10-16.
**Scope:** the platform only — what Meta and Kapso make possible. Competing chatbot products and hotel ops/revenue are covered by sibling documents.

## 0. Method and source discipline

| Tier | Sources used | How treated |
|---|---|---|
| Primary | `developers.facebook.com/documentation/business-messaging/whatsapp/*` (the `.md` variants of each page), Meta changelog, Meta Health Status docs | Authoritative |
| Primary (middleware) | `docs.kapso.ai` | Authoritative for what Kapso exposes |
| Secondary | Twilio, respond.io, Bird, Chatfuel, 360dialog, Wati, bixtech, ycloud, ChatMaxima | Labelled **(secondary)** inline; used only where Meta publishes nothing fetchable (rate-card figures, verification SLAs, free-allowance mechanics) |

`(inf.)` marks anything I inferred rather than read.

**Two caveats on freshness.** (1) Meta's own pages are internally inconsistent about the 1 Oct 2026 service-message change — see §6.2; I resolved it with Kapso's billing docs, which are dated past the cutover. (2) Meta's public changelog stops at 12 May 2026, so mid-2026 onward is reconstructed from the individual doc pages and Kapso.

**Search budget note:** this audit used its full web-search allowance. Three things stayed unresolved and are flagged as such: Meta's published MYR rate-card figures (vendor-sourced only), the current status of WhatsApp Pay in Singapore (sources conflict), and whether Cloud API has any native greeting/away-message feature (reasoned from the docs rather than confirmed by a dedicated page).

---

## 1. Harper's account state and exactly what it gates

Measured today: display name `Business Manager #2` **unapproved**; WABA **APPROVED**; BUSINESS entity **LIMITED**; messaging limit **TIER_250**; quality **GREEN**; not an Official Business Account.

| Observed state | What it means | What it blocks |
|---|---|---|
| Display name unapproved | Health Status reports this as a `LIMITED` phone-number entity. Meta's own wording: *"Your display name has not been approved yet. Your message limit will increase after the display name is approved."* ([health-status](https://developers.facebook.com/documentation/business-messaging/whatsapp/support/health-status)) | Guests see the raw number, not the hotel name, at the top of the chat. Blocks Official Business Account. Holds the number at the bottom tier. |
| BUSINESS entity LIMITED | `can_send_message: LIMITED` on the BUSINESS entity = the business portfolio meets requirements but carries a limitation, with `additional_info` explaining it. Meta documents the status model but not every cause; for an unverified portfolio the cause is business verification (inf. — Meta's health-status page only exemplifies LIMITED with the display-name case) | Overall health rolls up to LIMITED whenever any entity is LIMITED |
| TIER_250 | 250 unique recipients messaged **outside** a customer service window per moving 24 h. Since 7 Oct 2025 this is a **business-portfolio** limit, not a per-number one ([messaging-limits](https://developers.facebook.com/documentation/business-messaging/whatsapp/messaging-limits.md), [upcoming-messaging-limits-changes](https://developers.facebook.com/documentation/business-messaging/whatsapp/upcoming-messaging-limits-changes.md)) | Blocks the **Calling API** entirely (requires ≥2,000) |
| No templates of any category | Templates are the only message type sendable outside a customer service window ([pricing](https://developers.facebook.com/documentation/business-messaging/whatsapp/pricing.md)) | Harper **cannot open a conversation at all**. No booking confirmations, no pre-arrival, no post-stay. Also blocks broadcasts, Flows-as-template, carousel templates, and the Marketing Messages API |
| Not OBA | Requires verified portfolio + approved display name + 2SV + 30 days registered ([official-business-accounts](https://developers.facebook.com/documentation/business-messaging/whatsapp/official-business-accounts.md)) | Blocks the **Groups API** (OBA-only). No blue check. **Not discoverable in WhatsApp search** |
| Quality GREEN | Little to no negative feedback ([template-quality](https://developers.facebook.com/documentation/business-messaging/whatsapp/templates/template-quality.md)) | Nothing. This is the one asset worth protecting |

**The dependency chain, in one line:** business verification → tier 2,000 → display-name verification runs → (+30 days, +2SV) → OBA → Groups. Flows need verification. Calling needs tier 2,000. Everything needs templates first.

---

## 2. Conversation-opening: message templates

### 2.1 The three categories

Introduced June 2023 ([template-categorization](https://developers.facebook.com/documentation/business-messaging/whatsapp/templates/template-categorization)).

| Category | What it may say | What it may **not** say | Harper uses | Could | Cost (MY, secondary) |
|---|---|---|---|---|---|
| **Utility** | Triggered by a user action or request; must be non-promotional **and** either specific to/requested by the user or essential/critical. Allowed: opt-in/out confirmations, order & booking confirmations, shipping/status updates, refunds, payment reminders, balance alerts, setup prompts, feedback surveys **tied to a specific order or interaction**, moving a conversation to WhatsApp *if the user asked* | No promotion, recommendation, upsell, cross-sell, offers or renewal-seeking. Generic feedback surveys are not utility | No | **Yes — highest value** | RM 0.0564 |
| **Marketing** | The catch-all and most flexible: awareness, sales, retargeting, app promotion, relationship-building. Promotional discounts, product announcements, cart reminders, birthday/holiday greetings. **Mixed utility+marketing content, or unclear content (a bare placeholder, a generic greeting) lands here** | Subject to per-user delivery caps and native opt-out | No | Yes, after verification | RM 0.3467 (~6.1× utility) |
| **Authentication** | One-time passcodes only. Must come from the Template Library, must carry a copy-code or one-tap OTP button | No URLs, no media, no emojis anywhere in content or parameters; parameters capped at 15 chars | No | Not needed | RM 0.0564 / RM 0.1685 international |

Rates: vendor republication of Meta's MYR card, effective 1 Apr 2026 (**secondary** — [bixtech](https://bixtech.co/blog/whatsapp-business-api-pricing-malaysia), corroborated by several Malaysian resellers). MYR became a Meta billing currency on 1 Apr 2026 ([pricing](https://developers.facebook.com/documentation/business-messaging/whatsapp/pricing.md)). Meta's authoritative figures are in the MYR rate card linked from the pricing page, which is a CSV/PDF download I could not fetch.

### 2.2 Approval, review and what gets rejected

| Rule | Detail | Source |
|---|---|---|
| Review time | Up to 24 h, automated + manual. Appeals decided within 24 h | [template-review](https://developers.facebook.com/documentation/business-messaging/whatsapp/templates/template-review) |
| Creation rate limit | 100 templates per WABA per hour | [message-templates](https://developers.facebook.com/docs/whatsapp/business-management-api/message-templates) |
| **Template count cap** | **250 per WABA.** Vendors report a verified portfolio with one approved display name raises this to 6,000 (**secondary** — [Bird](https://bird.com/docs/knowledge-base/whatsapp/business-verification)); Meta's own page states only 250 | [whatsapp-business-accounts](https://developers.facebook.com/documentation/business-messaging/whatsapp/whatsapp-business-accounts.md) |
| Archival | Inactive 12 months → auto-archived; archived 28 days → deleted unless unarchived | [message-templates](https://developers.facebook.com/docs/whatsapp/business-management-api/message-templates) |
| Status values | `APPROVED` (shown as "Active – Quality pending"), `PENDING`, `REJECTED`, `PAUSED`, `DISABLED`. Only `APPROVED` can send | [template-review](https://developers.facebook.com/documentation/business-messaging/whatsapp/templates/template-review) |
| Notification | `message_template_status_update` webhook + WhatsApp Manager + email to Business Suite admins | same |

**Rejection reasons, verbatim-grouped** ([template-review](https://developers.facebook.com/documentation/business-messaging/whatsapp/templates/template-review)):

*Parameter formatting* — missing or mismatched curly braces; special characters (`#`, `$`, `%`) inside variables; non-sequential variables (`{{1}},{{2}},{{5}},{{4}}`); too many variables for the message length; **message starts or ends with a parameter**.
*Content/policy* — violates the Commerce Policy (anything naming goods/services with prices, fees, taxes or legal disclosures is treated as a transaction); violates the Business Policy by requesting full payment-card numbers, financial account numbers or national ID numbers, or documents likely to contain them (**partial identifiers such as last-4 are allowed**); abusive or threatening content, including threats of legal action or public shaming.
*Limits* — body character limits vary by format and tag; emoji count may be limited.
*Duplication* — same body **and** footer wording as an existing template is rejected (does not apply to `AUTHENTICATION`). The notification names the clashing template and language.
*Category* — `INCORRECT_CATEGORY` when Meta disagrees with the submitted category.

**Direct warning for Harper:** Harper's inbound flow collects ID photos and payment slips. That is fine for *inbound* media. But a template that **asks** for a national ID number, a full account number, or a document likely to contain one is an explicit rejection reason. Pre-arrival templates must ask the guest to *start a chat*, then collect documents inside the service window.

### 2.3 Automatic recategorisation and the misuse ladder

| Mechanism | Effect | Effective |
|---|---|---|
| Utility → marketing | Normally 1 day's advance notice; template stays APPROVED, category flips. **After a misuse warning, flips instantly with no notice** | Recurring process from 1 Jul 2024; instant-after-warning from 16 Apr 2025 |
| Utility submitted that should be marketing | Approved **as marketing** by default. `allow_category_change` is no longer needed — it is now default behaviour | 9 Apr 2025 |
| Marketing/utility → authentication | Advance notice; category does not change, but the template is set to `REJECTED` on the 1st of the following month and stops sending. **Not appealable** | 1 Oct 2024 |
| Appeals | Utility/marketing rejections and approved marketing templates are reviewable in Business Support → Template Category Updates → Request Review. 60-day window | — |

Misuse ladder (consistently labelling marketing as utility): Warning (instant recategorisation thereafter) → Rate limiting (utility capped in a rolling 24 h, min 7 days) → Utility restriction (all approved utility templates become marketing; new utility templates and category reviews disabled, 7 days, 30 for repeats) → Portfolio restriction (same across every WABA in the portfolio, 30 days). Reported by email and `account_update` webhook.

**Implication for a hotel:** the temptation is to dress a room-upgrade offer as a "booking update". Don't. One warning makes every later recategorisation instant and silent.

### 2.4 Template pacing and pausing

| Mechanism | Rule | Source |
|---|---|---|
| **Pacing** | Applies to marketing and utility. Messages send until a threshold, then are *held* for early feedback. Good feedback → released. Bad → status `PAUSED`, held messages dropped with error **132015**, admins notified. API shows `message_status: accepted` or `held_for_quality_assessment`. Meta aims to deliver held campaign traffic within an hour (p99). Utility is paced only *after* a utility template has been paused, for the following 7 days | [template-pacing](https://developers.facebook.com/documentation/business-messaging/whatsapp/templates/template-pacing.md) |
| **Pausing** | Triggered by a `RED` quality rating. 1st instance → **3 h**; 2nd → **6 h**; 3rd → **permanently disabled**. Auto-unpause after the duration, then the rating resets on recent feedback. Templates paused by *pacing* must be unpaused manually (`POST /{template_id}/unpause`) | [template-pausing](https://developers.facebook.com/documentation/business-messaging/whatsapp/templates/template-pausing.md), all businesses from 12 Oct 2023 |
| Portfolio pacing | Batches template delivery for large campaigns | Changelog, 8 Dec 2025 |

### 2.5 Template sub-types worth knowing

| Sub-type | Category | Notes | Kapso |
|---|---|---|---|
| Simple text / text header / media header | Any | — | `docs/whatsapp/templates/*` |
| **Location header** | **UTILITY or MARKETING** | Map header; tapping opens the device map app. Lat/long supplied **at send time**, not at creation. No real-time locations. Body ≤1024, footer ≤60 | `templates/location-header.mdx` |
| Media card carousel | **MARKETING only** | See §3.2 | `templates/carousel.mdx` |
| Coupon code | Marketing | Codes up to 20 chars (raised from 15 on 3 Dec 2025) | `templates/buttons.mdx` (inf.) |
| Limited-time offer | Marketing | Countdown UI | not separately documented (inf.) |
| Call-permission request | Marketing | Prerequisite for business-initiated calls | `whatsapp/calling/*` |
| Flow button (`sub_type: flow`) | Any | See §3.3 | `flows/sending-flows.mdx` |
| Authentication (OTP) | Authentication | Template Library only | `templates/authentication.mdx` |
| Catalog / SPM / MPM / product-carousel templates | Marketing/Utility | See §4.2 | not documented in Kapso |

**Location-header utility templates are the single best-fitting template type for a hotel** that Harper has not considered: an arrival-day utility template with a map header pointing at the property, sent the morning of check-in.

---

## 3. Rich message types (inside the 24-hour window)

Everything in this section is a **non-template** message and therefore requires an **open customer service window**. None of it needs Meta approval. This is the cheapest capability surface available to Harper right now.

### 3.1 What Harper already has, with the limits it may not know

| Type | Limits | Harper |
|---|---|---|
| Reply buttons | **3** buttons max; body ≤1024 (required); footer ≤60; label ≤20 and must be unique; button `id` ≤256; header optional (text/image/video/document) | ✅ Uses |
| List | **1–10 sections**, **1–10 rows total across all sections**; section title ≤24; row title ≤24; row description ≤72; row `id` ≤200; button text ≤20; body ≤4096; header ≤60 (text only); footer ≤60 | ✅ Uses |
| Text, image, location, location request, reaction, read receipts, typing indicator | Typing indicator auto-dismisses on reply **or after 25 s** | ✅ Uses |

**The 10-row ceiling is the one that bites a hotel.** A list cannot carry a 14-room-type menu or a full F&B menu. That is a structural argument for carousels or Flows, not for more lists.

### 3.2 What Harper is missing — free-form, no approval needed

| Capability | Limits | Could Harper? | What it takes | Kapso |
|---|---|---|---|---|
| **Interactive media carousel** (free-form) | **2–10 cards**; body ≤1024 required; **no** main header/footer/interactive components; every card needs an image or video header; card body optional ≤160 with ≤2 line breaks; each card needs one URL button **or** 1+ quick-reply buttons; **button types and counts must match across every card**; label ≤20; quick-reply id ≤256 | **Yes, today** | Nothing. No approval, no verification, no tier. Just an open window | ✅ `client.messages.sendInteractiveCarousel(...)` |
| **CTA URL button** | Body ≤1024 required; label ≤20 required and unique; footer ≤60; header ≤60 text or image/video/document (media header needs a public URL). Opens the device browser | **Yes, today** | Nothing | ✅ `sendInteractiveCtaUrl(...)` |
| Stickers | — | Yes | Nothing | ✅ `send-messages/sticker.mdx` |
| Contacts (vCard) | — | Yes | Nothing | ✅ `send-messages/contact.mdx` |
| Request contact info | — | Yes | Nothing | ✅ `send-messages/request-contact-info.mdx` |
| Address messages | — | Probably not useful for a hotel (inf.) | — | not documented |
| Video, audio, document | — | Yes | Nothing | ✅ |
| Contextual replies (quoting) | — | Yes | Nothing | `messages/contextual-replies.md` (Meta) |

**This is the headline finding of §3.** Harper's whole product lives inside the 24-hour window, and the free-form interactive carousel — the right control for showing 4 room types with photos and a "Check rates" button each — is available **right now** with no approval, no verification, and no tier change. Kapso exposes it directly. Harper's one carousel experiment went down the *template* path, which is the hard path and marketing-only.

**On that 24 Sep 9-card test:** HTTP 200 on template creation means Meta **accepted the submission**, not that it was approved, and certainly not that it renders. The status to check is `APPROVED` via `message_template_status_update`. There is also a specific trap Kapso documents: a carousel template approved with N cards **must be sent with exactly N cards**, or Meta returns error `(#132012)` with the misleading detail `header component parameter should not be empty`. For variable counts you need one approved template per count (`..._v1_2`, `..._v1_3`). ([Kapso carousel](https://docs.kapso.ai/docs/whatsapp/templates/carousel))

### 3.3 WhatsApp Flows

| Aspect | Detail | Source |
|---|---|---|
| What it is | Native multi-screen forms inside WhatsApp — lead capture, booking, surveys, registration, intake | [Kapso flows](https://docs.kapso.ai/docs/whatsapp/flows/overview) |
| **Requirement** | **A verified Meta Business Portfolio.** Meta's send guide also states "Verify your business and maintain high message quality" | Kapso (explicit), [sendingaflow](https://developers.facebook.com/documentation/business-messaging/whatsapp/flows/guides/sendingaflow) |
| Two send paths | Business-initiated: a template with a `FLOW` button (`sub_type: flow`, optional `flow_token`, `flow_action_data`). User-initiated: interactive message `type: flow` with `flow_message_version: "3"`, `flow_id`/`flow_name`, `flow_cta` (≤30 chars, no emoji), `flow_action` = `navigate` or `data_exchange`, `flow_action_payload` | same |
| Must be published | `mode` defaults to `published`; `draft` only for testing an edited published Flow | same |
| States | Draft, Published, Throttled, Blocked, Deprecated | Flows guides |
| **Platform support** | **Android ≥6.0 and iPhone ≥iOS 12 only. Flows do not work on WhatsApp Web or companion devices** | Flows overview |
| Encryption | Dynamic Flows need a data endpoint with Meta's business encryption set up | `flows/guides/whatsapp-business-encryption` |
| Metrics API | **Deprecated as of April 2026** | `flows/guides/metrics_api` |
| Kapso | Full: create, version, publish, data endpoints, encryption setup, static vs dynamic, TS SDK | `docs/whatsapp/flows/*`, `/api/meta/whatsapp/flows/*` |

**Static vs dynamic matters for Harper.** A static Flow (fixed screens, submit at the end) needs no data endpoint and no live inventory — a feedback form, a dietary/preferences intake, an arrival-details form. That is achievable the day verification lands. A dynamic Flow that shows live room availability needs an encrypted data endpoint wired to the PMS, which is an order of magnitude more work.

---

## 4. Commerce

### 4.1 WhatsApp Pay — the precise Malaysia answer

**Not available in Malaysia. Not close.**

Meta publishes payments documentation for exactly three markets, and the doc tree is the evidence:

| Market | Doc path | Rails | Status |
|---|---|---|---|
| **India** | `payments/payments-in/*` — overview, payment links, enhanced payment links, payment gateway, order-details & order-status templates, checkout-button templates | UPI only; INR only (`offset` 100); gateway deep integration limited to **Razorpay, PayU, Billdesk, Zaakpay**; UPI Intent works with any gateway supporting UPI Intent | Meta's own page says the feature **"is not publicly available yet"** and routes you to `whatsappindia-bizpayments-support@meta.com` |
| **Brazil** | `payments/payments-br/*` — orders, offsite Pix, boleto, one-click payments | Pix, boleto | Live. Direct in-chat **card** payments for new purchases ended **15 Jan 2026** (**secondary**, attributed to Meta's help centre — [getkanal](https://getkanal.com/blog/whatsapp-pay-2026)); Pix and payment links continue |
| **Mexico** | `payments/payments-mx/*` — overview, cash voucher | Cash voucher | Limited |

There is **no** `payments-my`, no `payments-sg`, no APAC payments tree, and no Malaysia mention anywhere in the payments docs. India's own API additionally hard-codes INR and an Indian beneficiary country with a 6-digit postal code, so it is not repurposable.

Singapore: sources genuinely conflict — some describe Stripe-processed business payments (cards + PayNow) from 2023, one lists consumer P2P via Singtel Dash, another lists it inactive. All are vendor blogs. Either way it is irrelevant to a Malaysian number, and **Meta publishes no Singapore payments documentation**, which is the strongest available signal that there is no API surface to build against.

**What Harper should do instead:** a **CTA URL button** to a hosted payment page (local gateway — iPay88, Billplz, Razer, Stripe MY). Free-form, no approval, works today inside the window, and Kapso exposes it. The payment confirmation then comes back as a utility template or a free-form reply.

### 4.2 Catalogs and product messages

| Capability | Detail | Harper |
|---|---|---|
| Catalog | Inventory uploaded to Meta (Commerce API or Commerce Manager) and linked to the WABA. Supports two categories: **products** (physical/digital goods) and **services** (appointments, consultations, subscriptions) | No |
| Message types | Catalog message (thumbnail of the whole catalog), single-product, multi-product (**up to 30 products in sections**), product carousel. Plus template variants of each | No |
| Commerce settings | `is_cart_enabled` (default `true`), `is_catalog_visible` (default **`false`**). `POST /{phone_number_id}/whatsapp_commerce_settings`. With catalog hidden, the storefront icon disappears and `wa.me` catalog links show "Invalid catalog link" | No |
| Cart | ≤99 units per item, unlimited distinct items. Carts are per chat thread **and per device**, never expire, cannot be edited once sent, and **a business cannot send a cart to a customer**. Cloud API chats **do not show the shopping-cart icon in the chat header** (unlike the WhatsApp Business app) | — |
| Enforcement | Items auto-reviewed against the Commerce Policy; violating items flagged; users can report products; appeals in Commerce Manager | — |
| Kapso | ✅ `sendInteractiveProduct(...)`, `sendInteractiveProductList(...)` with `catalogId` / `productRetailerId`. **No Kapso docs for catalog upload, commerce settings, or catalog/product templates** — that is a Kapso gap; do it in Commerce Manager or through the Meta proxy (inf.) | — |

**Verdict for a boutique hotel: low value, and Meta publishes no country-availability list for catalogs** beyond an India-specific compliance note. Room nights are date- and rate-dependent and the catalog has no availability model; the cart cannot be sent by the business; and the Cloud API doesn't even render the storefront icon. The "services" category could carry spa treatments, tours and airport transfers — fixed-price, non-dated items — which is the only sensible use. I could not confirm against Meta's own Commerce Policy page whether hotel/travel services carry any carve-out; vendor copies of the policy are silent on travel (**unresolved**).

---

## 5. Account features

| Feature | Rules and limits | Harper | Could | Takes | Kapso |
|---|---|---|---|---|---|
| **Business profile** | `about`, `address` (free text ≤256, **not validated**), `description`, `email`, `websites` (array), `vertical` (`WhatsAppVertical` enum, excluding `UNDEFINED`/`NOT_A_BIZ`), `profile_picture_handle` (write) / `profile_picture_url` (read). `POST /{phone_number_id}/whatsapp_business_profile`. No field is marked required | Minimum only | **Yes — today** | Nothing. Free, instant | ✅ `/api/meta/whatsapp/business-profile/*` |
| **Display name** | Changeable **10× per 30-day period**. Verification runs against the display-name guidelines; `phone_number_name_update` webhook fires with `decision` + `name_status`. `verified_name` shows the submitted string, **not** approval. After approval you must `POST /{phone_number_id}/register` within **14 days** or resubmit. Re-registering before approval does nothing. OBA numbers must change the name via direct support | **Unapproved placeholder** | **Must fix first** | Submit a real name. **Most complete in 24–48 h**; `deferred` usually resolves in a few days | ✅ `POST /platform/v1/whatsapp/{id}/display_names` |
| Display-name statuses | `submitted`, `pending_review`, `approved`, `available_without_review` (instant, common names), `deferred`, `declined` | — | — | — | Kapso documents all six |
| Display-name rejection reasons | `NAME_NOT_CONSISTENT` (must match website/branding), `NAME_FORMAT_UNACCEPTABLE` (no URLs, emails or promotional text), `NAME_EMPLOYEE_ISSUE` (no personal names), `NAME_ENDCLIENT_NOTRELATED` (must relate to the business) | — | — | — | ✅ Kapso lists them |
| **QR codes & short links** | `POST /{phone_number_id}/message_qrdls` with `prefilled_message` + `generate_qr_image` (`SVG`\|`PNG`). Returns `code`, `deep_link_url`, `qr_image_url`. **≤2,000 QR codes and short links per number**; prefilled message **≤140 chars**; codes never expire; editable and deletable later. **No scan analytics at all** — Meta limits logged data for privacy. SVG for print. Deleted codes show an expired-link error | No | **Yes — today** | Nothing. Free, instant, no approval | ❌ **Not in Kapso's documented proxy.** Use WhatsApp Manager / Business Suite, or the Meta proxy base URL (inf.) |
| Short links vs `wa.me` | Short links mask the phone number and let you edit or delete the prefilled message afterwards; a `wa.me` link embeds both permanently | No | Prefer short links | — | — |
| **Ice breakers** | **≤4 per number, ≤80 chars each, no emoji.** Shown the first time a user opens the chat. Tapping fires a normal `messages` webhook with the prompt in `text.body`. **Dismissed if the user arrives via a `wa.me`/`api.whatsapp.com` link with pre-filled text** | No | **Yes — today** | Nothing. WhatsApp Manager → Phone number → Automations, or `POST /{phone_number_id}/conversational_automation` | ❌ Not in Kapso docs |
| **Commands** | **≤30 commands**, name ≤32 chars, hint ≤256 chars, no emoji. Surfaced when the user types `/`. Full typed text arrives in `text.body` | No | Yes — today | Same | ❌ Not in Kapso docs |
| **Greeting / away messages** | **Do not exist on the Cloud API.** These are WhatsApp Business *app* features. On Cloud API the equivalent is ice breakers (first-open prompts) plus your own out-of-hours logic. (inf. — reasoned from the conversational-components page covering only ice breakers and commands, and no Cloud API page documenting them; not confirmed by a dedicated Meta page) | Own code | Keep in own code | — | Kapso workflows/agents |
| **Labels** | **Do not exist on the Cloud API.** A WhatsApp Business app feature. Cloud API equivalents are your own CRM tags, Kapso contacts, and Kapso conversation assignment/status | Own code | Kapso's own primitives | — | ✅ `whatsapp_contacts`, `conversation_assignments`, `set_conversation_status` |
| **Business username** | Reserve/read/change/delete a username for a number; `transfer_action` `none`\|`force_transfer` within the same portfolio; `username_suggestions` endpoint | No | Yes | Reserve early — namespace is first-come (inf.) | ✅ `api.kapso.ai/meta/whatsapp/v24.0/{id}/username` |
| **Broadcasts** | **Template-only** — Meta requires an approved template to open a conversation, so free-form cannot be broadcast. ≤1,000 recipients per API request. Lifecycle `draft`→`scheduled`→`sending`→`completed`/`stopped`/`failed`. Per-recipient delivery/read/reply tracking; `suppressed_count` for marketing opt-outs | No | After templates + verification | An approved template + opt-in | ✅ Full Kapso feature (CSV upload + API) |
| **Click-to-WhatsApp ads** | Opens a **72-hour free entry point window** when the user taps through from a CTWA ad or a Facebook Page CTA button **on Android or iOS** (desktop and web not supported). Welcome Message Sequences (text + prefilled message + FAQs) attach to the ad; need `whatsapp_business_management`; a sequence linked to a live ad must be disconnected before editing | No | Yes | An ad budget | Conversion events: ✅ `/api/meta/whatsapp/conversion-events/*` |

---

## 6. The APIs around them

| API | What it gives | Harper | Kapso |
|---|---|---|---|
| **Message status webhooks** | `sent`, `delivered`, `read`, `played` (voice note first play), `failed`. A status is only `read` if delivered, so a `delivered` webhook can be skipped when read instantly. **`pricing` object** (on `sent`, alongside `delivered`/`read`): `pricing_model` `PMP` (`CBP` only on webhooks before 1 Jul 2025); `type` ∈ `regular`, `free_customer_service`, `free_entry_point`; `category` ∈ `authentication`, `authentication-international`, `marketing`, `marketing_lite`, `referral_conversion`, **`service`**, `utility`; `billable` (boolean, **being deprecated** — use `type` + `category`). **`conversation` object**: from v24.0 it is **omitted entirely unless the message was sent in an open free entry point window** | Unknown — **verify** | ✅ Kapso webhooks + `list_whatsapp_messages` |
| **Marketing Messages API** (was MM Lite) | `POST /{phone_number_id}/marketing_messages`. Delivery optimisation, benchmarks, recommendations, creative optimisation (in test), richer media incl. GIFs, time-to-live, and a **max price per marketing message** (2026). Same billing model and a similar schema to Cloud API; reuses existing numbers and marketing templates. Eligibility: active WABA in an eligible country + an approved marketing template + `messages` webhook subscribed + ToS accepted in the App Dashboard. Check `marketing_messages_onboarding_status` on the WABA. **Malaysia is fully supported** (not on any exclusion list). Degraded in EEA/UK/JP/KR/NG/ZA (no optimisation, no click/conversion reporting). **US WhatsApp users cannot receive marketing messages at all — error 131049, from 1 Apr 2025.** Blocked entirely for Cuba, Iran, North Korea, Syria, Venezuela, Crimea/Donetsk/Luhansk. GA **February 2026** (**secondary**; Meta's own page doesn't state a GA date) | No | ✅ `/api/meta/whatsapp/messages/send-a-marketing-message` |
| **Typing indicator + read receipts** | Single call: `POST /{phone_number_id}/messages` with `status: "read"`, `message_id`, `typing_indicator: {type: "text"}`. Dismisses on reply **or after 25 s** | ✅ Uses | ✅ `mark-read.mdx` |
| **Block Users** | `POST`/`DELETE`/`GET /{phone_number_id}/block_users`. **Only users who messaged in the last 24 h can be blocked.** Cannot block another WABA. ≤1,000 users per request; blocklist cap **64,000**. Errors: 139100 (partial failure), 139101 (cap), 139102 (list changed mid-pagination), 139103 (retry), 130429 (rate limit), 131021 (own number), 131047 (re-engagement required) | No | **Yes** — a real abuse control | ✅ `/api/meta/whatsapp/block-users/*` |
| **Conversational Automation** | Ice breakers + commands (§5) | No | ❌ |
| **Health Status** | `health_status` on BUSINESS / WABA / APP / PHONE_NUMBER / MESSAGE_TEMPLATE. `can_send_message` ∈ `AVAILABLE`, `LIMITED` (+`additional_info`), `BLOCKED` (+`errors` with code and suggested fix). Any BLOCKED node → overall BLOCKED; else any LIMITED → overall LIMITED | Should poll | ✅ `GET /whatsapp/phone_numbers/{id}/health` (cached 3 min; 5 rps / 60 rpm per project) |
| **Calling API** | GA **15 Jul 2025**. User-initiated available wherever Cloud API is; **business-initiated available everywhere except US, Canada, Egypt, Vietnam, Nigeria** — Malaysia is fine. **Requires a daily messaging limit of ≥2,000** → **blocked for Harper today.** Needs the `calls` webhook field, `whatsapp_business_messaging` permission, and calling enabled on the number. Call permissions: production **1 request/day, 2/week** per user pair; a reconsider system message after 2 consecutive unanswered/rejected calls; **auto-revoked after 4 consecutive unanswered**. Business-initiated calls raised to 100/user/day on 19 Dec 2025. User-feedback restrictions from 27 Jan 2026; low-pickup-rate restrictions from 5 Sep 2025. Video calling, recording, transcription and SIP all documented | No | Only after tier 2,000 | ✅ Kapso proxies call actions and forwards events; **you supply the media server / WebRTC + SDP**. Sandbox does not support calling. Enable via `calls_enabled` |
| Calling cost | User-initiated **free**. Business-initiated **per minute** by called country and monthly volume tier, **billed in 6-second pulses rounded up** (a 56 s call = 10 pulses). Native recording/transcription currently free, with Meta planning separate pricing. **Call permission requests are messages and are billed as messages** | — | ✅ [Kapso pricing FAQ](https://docs.kapso.ai/docs/whatsapp/pricing-faq) |
| **Groups API** | Open to **all businesses with OBA**. ≤**8 participants** per group, ≤10,000 groups per number. Invite-only via invite link. Text, media, and text/media templates only — **no interactive messages, no auth, no commerce, no calling, no disappearing/view-once**. Cannot hide the participant list, edit or delete messages. One Cloud API business per group. **No template performance metrics in groups.** Per-message pricing applies. A message from any group member opens/refreshes the service window between the business and the **whole group** | No | Only after OBA | ❌ Not in Kapso docs |
| **Business-scoped user IDs (BSUID)** | Addressing users without a phone number | — | ✅ `business-scoped-user-ids.mdx`, `recipient` param |
| **Throughput** | 1,000 msg/s tier needs: portfolio at UNLIMITED, the number messaging ≥100K unique users outside CSWs in a moving 24 h, and Medium+ quality. Upgrade within 12 h | Irrelevant | — |
| **Meta Business Agents** | Platform launched **1 Jul 2026**; charged **per token** from **1 Aug 2026**, and **not free even inside the 72-hour free entry point window** | No | ✅ `meta-business-agents.mdx` |

---

## 7. The rules that actually bite

### 7.1 The 24-hour customer service window — and exactly what reopens it

| Rule | Detail | Source |
|---|---|---|
| What opens it | **An inbound message from the WhatsApp user.** Nothing else | [pricing](https://developers.facebook.com/documentation/business-messaging/whatsapp/pricing.md) |
| What reopens it | **Only another inbound message from the user.** Every inbound message restarts the 24-hour clock | same + vendor consensus |
| What does **not** reopen it | Sending a template. Sending anything at all. A delivery or read receipt. Time passing. A template can reopen it only *indirectly*, by prompting the guest to reply | (inf., from the rule that only templates are sendable outside the window) |
| Inside the window | Any message type: free-form text, media, interactive lists/buttons/CTA URL/carousel/Flows, reactions | — |
| Outside the window | **Templates only.** Free-form sends are rejected | [pricing](https://developers.facebook.com/documentation/business-messaging/whatsapp/pricing.md) |
| Groups | A message from **any** group member opens or refreshes the window between the business and the entire group | Groups docs |
| Free Entry Point window | A tap-through from a **Click-to-WhatsApp ad or a Facebook Page CTA button on Android/iOS** (not desktop/web). Reply within 24 h → that reply is free and opens a **72-hour FEP window** in which **all message types are free, including templates**. The CSW and the FEP window run **independently** — when the CSW closes you can still only send templates | [pricing](https://developers.facebook.com/documentation/business-messaging/whatsapp/pricing.md) |

One vendor states the CTWA free window is 7 days rather than 72 hours ([respond.io](https://respond.io/blog/whatsapp-pricing-change-2026)). **Meta says 72 hours on its own pricing page, twice.** Use 72 hours.

### 7.2 Pricing — what is true in October 2026

| Date | Change | Source |
|---|---|---|
| 1 Nov 2024 | Service conversations became free for all businesses, including AI-enabled experiences | Changelog |
| **1 Jul 2025** | **Per-message pricing replaced conversation-based pricing.** Only *delivered* template messages are billed. Rate = template category × recipient country calling code. Inbound messages are never charged | [pricing](https://developers.facebook.com/documentation/business-messaging/whatsapp/pricing.md) |
| 1 Oct 2025 | `VOLUME_BASED_PRICING_TIER_UPDATE` webhooks began | same |
| 1 Jan 2026 | India marketing ↑; France & Egypt marketing ↓; North America utility & auth ↓; India billing → INR | same |
| 16 Feb 2026 | AI Providers pricing policy took effect (updated 12 May 2026) | same |
| 13 May 2026 | AI Providers no longer charged for non-template messages to EU/EEA users (Brazil charges remain) | Changelog |
| **1 Apr 2026** | **MYR added as a billing currency** (with ARS, CLP, COP, PEN, SAR, SGD, AED). Saudi marketing ↑, India auth-international ↑, Pakistan utility/auth ↑, Turkey utility/auth ↓ | [pricing](https://developers.facebook.com/documentation/business-messaging/whatsapp/pricing.md) |
| 1 Jul 2026 | New rate cards + volume tiers. Italy, Spain, UK marketing ↑; Poland ↓. Brazil → BRL | same |
| 1 Jul 2026 | Meta Business Agent Platform launched | [non-template-messages](https://developers.facebook.com/documentation/business-messaging/whatsapp/pricing/non-template-messages.md) |
| 1 Aug 2026 | Meta Business Agent messages charged **per token**, not free in either window | same |
| **1 Oct 2026** | **Service messages became billable, and utility templates inside the 24-hour window became billable.** Meta's wording: *"Effective October 1, 2026, Meta will charge for service messages, which have not been charged since November 2024."* Charged per message, like templates | same |
| 31 Dec 2026 | Deadline for India WABAs to migrate to INR (hard cutoff 1 Jan 2027) | [pricing](https://developers.facebook.com/documentation/business-messaging/whatsapp/pricing.md) |

**Resolving Meta's own contradiction.** `pricing.md` still reads *"All non-template messages are free"* and shows a `free_customer_service` / `billable: false` example — that page has not been updated past the cutover. `pricing/non-template-messages.md` carries the dated rule and is still phrased in the future tense. The tie-breaker is Kapso, whose billing docs are written from the far side of the change:

> "Non-template messages are billed by Meta as the service category **since October 1, 2026**." — [Kapso, Meta message billing](https://docs.kapso.ai/docs/whatsapp/meta-message-billing)

> "Activation happens at **00:00 on October 1 in each WhatsApp Business Account's own timezone**, and each message is priced on **the date it was delivered in that timezone** — not when you sent it or when Kapso processed it." — [Kapso, Pricing FAQ](https://docs.kapso.ai/docs/whatsapp/pricing-faq)

**The free service-message allowance:**

| Rule | Detail | Source |
|---|---|---|
| Size | **1,000 free delivered service messages per business phone number per calendar month** | Kapso pricing FAQ; corroborated by respond.io, ycloud, Twilio (**secondary**). **Not findable on Meta's own pricing page** — flag for re-check |
| Scope | Per **phone number**, not per WABA. Shared across individual and group messages, and across all recipient markets — not renewed per country | Kapso; [Kapso pricing guide](https://kapso.com/guides/whatsapp-pricing/october-1-2026/service-message-pricing) |
| Rollover | **None.** Resets each calendar month | same |
| Who decides | **Meta** classifies which deliveries fall inside the allowance and reports it back **after delivery**. The `pricing.type` flips from `free_customer_service` to `regular` while `category` stays `service` | same |
| Rate | **The service rate equals the utility rate in every market Meta publishes** on the October card — there is no separate service row | Kapso pricing FAQ (explicit); also asserted by bixtech (**secondary**) |
| Utility-in-window | **Billable from the first message**, with **no** free allowance | respond.io, Kapso (**secondary + middleware**) |
| Still free | Inbound messages. Reactions. Everything inside an open FEP window (except Meta Business Agent messages) | Kapso; [pricing](https://developers.facebook.com/documentation/business-messaging/whatsapp/pricing.md) |

**Volume tiers** apply to **utility and authentication only** (and now service, by inheritance of the utility rate — inf.). Aggregated across all WABAs in a portfolio, per market per category; only *charged* messages count, so free-CSW utility and FEP messages don't; reset monthly at 00:00 in the WABA's timezone.

**What this costs Harper.** Harper's entire product is free-form service messages inside the window — precisely the category that stopped being free 15 days ago. At RM 0.0564 (**secondary**) and 1,000 free per month, a quiet month costs nothing; past 1,000 outbound messages it is roughly **RM 56 per additional 1,000**. That is small, but it is no longer zero, and it now scales with chattiness — so a verbose agent that sends five bubbles where one would do costs 5× past the threshold. **Message consolidation is now a cost lever, not just a UX preference.**

**Kapso operational consequences worth knowing:**
- Because Meta only reports billability after the fact, Kapso does not hold credits up front for a service send. Sends proceed while the balance is positive and settle afterwards.
- If a balance sync finds the project at or below zero **and** a settled service charge exists, Kapso pauses potentially-paid sends on **every number in the WABA** with reason `service_credits_exhausted`. Service sends are then rejected **even if they would have turned out free**. Reactions are exempt and never paused.
- Service billing needs Meta's published service rate for the recipient's market **and a supported WABA timezone**; otherwise the send is rejected with a `service_`-prefixed code and HTTP **402** rather than charged at a guessed rate.
- Non-USD WABAs carry an **FX margin (5% at launch)**; Tech-Provider-infrastructure sends add a **5% managed billing fee**.
- **You cannot switch a WABA from Kapso's shared credit line back to a Meta card** — Meta doesn't support it. That requires a new WABA and a number migration. Decide the billing mode before committing.

### 7.3 Marketing-message limits and opt-out obligations

| Rule | Detail | Source |
|---|---|---|
| **Per-user marketing cap** | **Adaptive, no published number.** Meta limits how many marketing templates a given user receives *from any business* over a period, based on that user's recent marketing read rate and overall message volume from friends, family and businesses. Adjusts automatically | [per-user-limits](https://developers.facebook.com/documentation/business-messaging/whatsapp/templates/marketing-templates/per-user-limits.md) |
| What counts | Every **delivered** marketing template. **Marketing messages sent inside an open 24-hour window do not count** | same |
| Exclusions | Caps are not active for business numbers in, or users in, the **EEA, UK, Japan, South Korea**. Malaysia **is** subject to them | same |
| **US** | Marketing templates are **not delivered to US numbers at all** (error **131049**) | same; MM API docs date this to 1 Apr 2025 |
| Error + retry | Error **131049** with a `failed` status webhook. **Wait ≥24 h before resending.** Repeated retries within 24 h can make further delivery to that user unavailable for up to 24 h | same |
| **Opt-in requirement** | You may message someone only with their mobile number **and** opt-in permission for **your specific business**. Opt-in may be general rather than WhatsApp-specific if local law allows. Any method (SMS, website, IVR, in-person/paper) provided it: (a) clearly states the person is opting in to receive communication from the business, and (b) **clearly states the business name**, plus any notices or permissions local law requires | [getting-opt-in](https://developers.facebook.com/documentation/business-messaging/whatsapp/getting-opt-in.md) (Business Messaging Policy updated Nov 2024) |
| Opt-out guidance | Meta *recommends* clear opt-out instructions **by message category** and honouring them. Sustained low quality → rate limiting | same |
| **Native opt-out** | WhatsApp lets users stop marketing messages from a business number **without blocking it**. Reported by the **`user_preferences` webhook** with values `stop` / `resume`, `category: marketing_messages`, `wa_id`, `timestamp`. Does **not** fire for "Interested"/"Not interested" feedback | [user_preferences](https://developers.facebook.com/documentation/business-messaging/whatsapp/webhooks/reference/user_preferences.md) |
| Enforcement | Sending marketing to a stopped contact fails with Meta error **131050** | Kapso marketing-opt-outs |
| Scope | **MARKETING-category templates only.** Utility and authentication templates and free-form in-window messages always go through. **Scoped to the specific number** the contact stopped | same |
| **No API to opt back in** | The preference can only be set by the contact, inside WhatsApp. **There is no API or dashboard control to opt a contact out or back in.** To resume, the contact taps *Resume promotions* | same |

**Harper's gap here is real and specific.** Harper handles STOP/START in its own code. That is a different mechanism from Meta's native opt-out and does not cover it. A guest who taps WhatsApp's own "stop promotions" is invisible to Harper's homegrown list; Harper will keep attempting marketing sends and collecting `131050` failures, which is both a compliance and a quality problem. Kapso already solves this: it records stops from three signals (`meta_webhook`, `meta_delivery_error` on a 131050 status webhook, `meta_synchronous_error` on a rejected broadcast send), exposes `GET /platform/v1/whatsapp/contacts/{id}/marketing_preferences` with a `marketing_allowed` boolean to branch on, fires `whatsapp.contact.marketing_preference_changed`, returns **422** `marketing_preference_stopped` before billing (so refused sends are never charged), and marks broadcast recipients `suppressed`. Harper should branch on `marketing_allowed` and keep its own STOP/START only as an additional, broader preference layer.

### 7.4 Messaging tiers and lifting the number out of TIER_250

Restructured **7–8 Oct 2025**: limits moved from individual phone numbers to **business portfolios**, and all numbers in a portfolio share one limit.

| Tier | Limit (unique numbers / 24 h, messaged outside a CSW) | How reached |
|---|---|---|
| Starting | **250** | Default for a newly created business portfolio |
| 2nd | **2,000** | Complete a scaling path, or automatic scaling |
| 3rd | 10,000 | Automatic scaling |
| 4th | 100,000 | Automatic scaling |
| 5th | Unlimited | Automatic scaling |

**Paths to 2,000 — any one of:** (a) verify your business; (b) have your partner verify your business, if a partner onboarded you (Kapso supports partner-led verification); (c) deliver 2,000 messages outside customer service windows to unique numbers within a **moving 30-day** period using **high-quality templates**. After you complete a path, Meta reviews message quality and approves or denies eligibility for automatic scaling.

**Automatic scaling from 2,000 up — both required:** high-quality messages across all numbers and templates, **and** at least **half** your current limit used in the **last 7 days**. When both hold, the limit rises **one level within 6 hours** (was 24 h).

Other changes from the same release: new phone numbers inherit the portfolio's existing limit instead of starting at 250; the automatic-scaling threshold rose from 1,000 to 2,000; the **Flagged quality state was removed**; and **quality drops no longer downgrade the messaging limit**. New field `whatsapp_business_manager_messaging_limit`; `messaging_limit_tier` is deprecated; `max_daily_conversation_per_phone` and `current_limit` report portfolio values and are **removed in February 2026**; `business_capability_update` v24.0+ uses `max_daily_conversations_per_business`.

**The exact sequence for Harper:**

1. **Change the display name.** `Business Manager #2` is a Meta placeholder and will fail `NAME_NOT_CONSISTENT` / `NAME_ENDCLIENT_NOTRELATED`. Submit the hotel's trading name exactly as it appears on its website and signage. No URLs, no emails, no promotional words, no personal names. Via Kapso: `POST /platform/v1/whatsapp/{phone_number_id}/display_names`. **24–48 h** typical; `available_without_review` is instant for common names; `deferred` usually clears in a few days without action. Budget is limited to 10 changes per 30 days, so get it right. **Note:** Meta also runs display-name verification automatically once you reach a higher messaging limit — so step 2 can re-trigger it.
2. **Verify the Meta Business Portfolio** at `business.facebook.com/latest/settings/security_center`. This is the item that clears BUSINESS=LIMITED, and it is simultaneously a scaling path to 2,000 and a hard prerequisite for Flows. Documents: one proving legal identity (certificate of incorporation / business licence / SSM registration / tax registration) and one proving address or phone (recent utility bill, bank statement within 3 months, lease, official phone bill). **The legal business name, address and phone must match the Meta Business Portfolio fields exactly** — mismatch is the most common rejection cause. Timing (**secondary**): minutes-to-hours on the light path, 1–5 business days typically, up to 14 business days where a website and identity check are added; appeals up to 14 days. One Meta community report sat "In Review" for 3.5 months, so do not sequence anything critical behind it. If Kapso onboarded Harper, **partner-led business verification** is an alternative path.
3. **Portfolio limit → 2,000** on verification, after Meta's quality review. This is also where the Calling API becomes available.
4. **Create 2–3 high-quality utility templates** (§8). Needed before any volume path matters, and needed to open conversations at all.
5. **Then automatic scaling does the rest** — but note the gate: you must *use* ≥50% of your limit over 7 days. A boutique hotel will sit at 2,000 indefinitely, which is **far more than enough**. Do not chase higher tiers.
6. **OBA**, if the blue check and WhatsApp-search discoverability are wanted: verified portfolio + approved display name + **two-step verification enabled on the number** + **30 days registered** on the platform. Request via WhatsApp Manager → Overview → number → Profile → Official business account → Submit Request, or the OBA Status API. **A rejected request means a 30-day wait before reapplying.**

**Do not take path (c).** 2,000 unique recipients in 30 days through a 250/day ceiling is arithmetically possible but requires templates, opt-ins and real volume a boutique hotel does not have. Verification is faster and cheaper.

### 7.5 Quality rating and what drops it

| State | Meaning | Consequence |
|---|---|---|
| `GREEN` | High — little to no negative feedback | Sendable |
| `YELLOW` | Medium — negative feedback from multiple users, or low read rates | Sendable; "may soon become paused or disabled" |
| `RED` | Low — same causes, worse | Sendable but "in danger of being paused or disabled soon"; **triggers the pause ladder** |
| `UNKNOWN` | No feedback or read-rate data yet. All new templates start here | Sendable |

Meta publishes **no thresholds or scoring formula** — ratings update automatically from usage, customer feedback and engagement. What drops it: **negative user feedback (blocks and reports) and low read rates**. Quality feeds template pacing and pausing. Since 7 Oct 2025, quality drops **no longer downgrade the messaging limit** — but they still pause and ultimately disable templates, and sustained low quality still invites rate limiting at the account level.

Monitor: `message_template_quality_update` and `phone_number_quality_update` webhooks.

**Policy enforcement ladder** (separate from quality): Warning → 1 or 3 day block on all template categories and on adding numbers → 5, 7 or 30 day block on sending **any** messages → indefinite account lock, removable only by appeal → permanent disablement. Appeals via Business Support Home "Request Review", decided in **24–48 h**, result "Unchanged" or "Reversed". Not all spam violations are appealable. Immediate offboarding for severe harm.

**What this means for Harper in practice:** GREEN with low volume and no templates is an untested rating. The moment Harper starts sending templates, every template begins at `UNKNOWN` and earns its own rating. The real risks for a hotel are (1) sending pre-arrival messages to guests who never opted in, (2) sending a "booking update" that is actually an upsell, and (3) sending to stale numbers from an old PMS export. All three produce blocks and reports, which is the only input that matters.

---

## 8. For a small hotel: what is worth having, in order

A boutique hotel with one number and low volume should build roughly six things, not twenty. Ranked by value ÷ effort.

### Tier 1 — do now. Free, no approval, no verification, days of work.

| # | Capability | Why for this hotel | Blocker | Kapso |
|---|---|---|---|---|
| 1 | **Fix the display name** | Guests currently see a raw US number from a Sabah hotel. This is the single worst trust signal in the account, and it gates OBA and the tier ladder | None | ✅ |
| 2 | **Fill in the Business Profile** | `address`, `description`, `websites`, `email`, `vertical`, profile picture. Free, instant, and the first thing a guest taps | None | ✅ |
| 3 | **Free-form interactive carousel** for room types / F&B / tours | Solves the 10-row list ceiling. 2–10 image cards with a quick-reply or URL button each. **No template, no approval, no verification** | None — an open window is all it needs | ✅ `sendInteractiveCarousel` |
| 4 | **CTA URL buttons** | Booking engine, payment page, menu PDF, Google Maps — without pasting raw URLs. This is also Harper's **answer to WhatsApp Pay not existing in Malaysia** | None | ✅ `sendInteractiveCtaUrl` |
| 5 | **Ice breakers (≤4) + commands (≤30)** | A guest opening the chat cold sees four taps — "Check in early", "Book airport transfer", "Restaurant hours", "Wi-Fi password" — instead of a blank box. Per-language sets are not supported, so pick the dominant language or keep them bilingual and short (inf.) | None | ❌ Meta direct / WhatsApp Manager |
| 6 | **QR codes + short links** with prefilled messages | Table tents, room keycard sleeves, lift lobby, airport pickup signs, OTA confirmation emails. Distinct codes per placement, each with its own prefilled text, so the inbound message tells you where the guest scanned. **No scan analytics** — the prefilled text *is* your attribution | None | ❌ Meta direct / WhatsApp Manager |
| 7 | **Native marketing opt-out handling** | Replace/augment the homegrown STOP/START: subscribe to `user_preferences`, branch on Kapso's `marketing_allowed`, handle 131050. Compliance, not nice-to-have | None | ✅ |
| 8 | **Audit the `pricing` object on status webhooks** | From 1 Oct 2026 this is how you learn whether a reply was free or billed. Log `pricing.type` and `pricing.category` per message and watch the 1,000/month line | None | ✅ |

### Tier 2 — after business verification.

| # | Capability | Why | What it takes |
|---|---|---|---|
| 9 | **Business portfolio verification** | Clears BUSINESS=LIMITED, lifts the portfolio to 2,000, and unlocks Flows and the OBA path. **The keystone item** | SSM/incorporation doc + address proof matching the portfolio exactly |
| 10 | **2–3 utility templates** — booking confirmation, arrival-day (with a **location header**), post-stay folio/receipt | The only way Harper can open a conversation at all. Cheapest category (~RM 0.056). Must be strictly non-promotional and tied to a specific booking | Opt-in at booking naming the hotel; ≤24 h review |
| 11 | **One static WhatsApp Flow** — arrival details / dietary & preferences / post-stay feedback | Replaces a 12-turn interrogation with one form. No data endpoint, no PMS integration. **Remember: Flows do not render on WhatsApp Web** — keep a conversational fallback | Verified portfolio; published Flow |
| 12 | **Two-step verification on the number** | Prerequisite for OBA, and basic security hygiene | None |

### Tier 3 — considered, with a reason to wait.

| # | Capability | Verdict |
|---|---|---|
| 13 | **Click-to-WhatsApp ads** | The strongest *economic* argument on this list: a CTWA tap-through opens a **72-hour window in which every message type is free, including templates**, and free-entry-point traffic doesn't count toward volume tiers. If the hotel already buys Meta ads, route them to WhatsApp. If it doesn't, this is a marketing decision, not a platform one |
| 14 | **Marketing templates + broadcasts** | Only with genuine, documented opt-in. 6× the price of utility, subject to adaptive per-user caps, and the main way to earn blocks and wreck a GREEN rating. A 40-room hotel's marketing list is small enough that the downside outweighs the upside until the basics are solid |
| 15 | **Official Business Account** | Worth having for the blue check and because **non-OBA numbers do not appear in WhatsApp search**. Requires +30 days and 2SV. A rejected request costs a 30-day wait, so apply once, properly |
| 16 | **Business username** | Cheap to reserve, and namespaces are first-come (inf.). Low effort, low urgency |
| 17 | **Carousel *templates*** (marketing) | Only after free-form carousels have proved the format. Marketing-only, marketing-priced, and carry the fixed-card-count trap |
| 18 | **Calling API** | Genuinely useful for a hotel (front-desk voice without a PBX), but needs tier ≥2,000, your own media server/WebRTC stack, and a voice runtime you pay for separately. Billed per 6-second pulse. **Park until Tier 2 is done** |
| 19 | **Groups API** | A per-booking group for a family or tour party is an appealing idea, and **≤8 participants** actually fits. But it needs OBA, allows **no interactive messages**, and gives no template metrics. Watch it |

### Not worth building

| Capability | Why not |
|---|---|
| **Catalogs / product messages** | No availability model for dated room nights; the business cannot send a cart; the Cloud API doesn't render the storefront icon. The "services" category could hold spa/tours/transfers — marginal. Kapso documents the *send* side but not catalog upload or commerce settings |
| **WhatsApp Pay** | Does not exist in Malaysia (§4.1). Use a CTA URL to a local gateway |
| **Authentication templates** | Harper has no login to protect |
| **Marketing Messages API** | Delivery optimisation for campaigns at scale. Harper has no campaigns and no scale. Revisit if marketing volume ever justifies it |
| **Throughput upgrade** | Needs 100K unique users / 24 h |
| **Meta Business Agents** | Per-token billing from 1 Aug 2026 and **not free even inside the FEP window**. Harper already has its own agent |

---

## 9. What is NOT possible — so nobody plans around it

| Common assumption | Reality | Source |
|---|---|---|
| "We can message a guest whenever we like." | Only inside a 24-hour window opened **by the guest's own inbound message**, or via an approved template. There is no third option | [pricing](https://developers.facebook.com/documentation/business-messaging/whatsapp/pricing.md) |
| "Sending a template reopens the window." | **It does not.** Only an inbound user message opens or reopens the window. A template can reopen it only indirectly, by getting the guest to reply | inf. from the above |
| "Service replies are free." | **Was true. False since 1 October 2026.** 1,000 free delivered service messages per phone number per month, then billed at the utility rate. Utility templates inside the window are billable **from the first message**, with no allowance | [non-template-messages](https://developers.facebook.com/documentation/business-messaging/whatsapp/pricing/non-template-messages.md), Kapso |
| "We can take payment in WhatsApp in Malaysia." | **No.** Meta publishes payments APIs for India (itself "not publicly available yet"), Brazil and Mexico only. No Malaysia, no Singapore, no APAC tree | payments doc tree |
| "We can broadcast a free-form message / an image to past guests." | **No.** Broadcasts are **template-only**. Free-form cannot open a conversation | [Kapso broadcasts](https://docs.kapso.ai/docs/platform/broadcasts/overview) |
| "HTTP 200 on template creation means it works." | 200 means **submitted**. Approval is a separate, up-to-24-hour decision reported as `APPROVED` via `message_template_status_update`. And approval still doesn't prove rendering | [template-review](https://developers.facebook.com/documentation/business-messaging/whatsapp/templates/template-review) |
| "A carousel template can show however many cards we have." | **No.** The card count is **fixed at creation**. Send fewer and you get error `(#132012)` with the misleading detail `header component parameter should not be empty`. One template per supported count | [Kapso carousel](https://docs.kapso.ai/docs/whatsapp/templates/carousel) |
| "Lists can hold our whole menu." | **Max 10 rows total across all sections** — not 10 per section | [interactive-list-messages](https://developers.facebook.com/documentation/business-messaging/whatsapp/messages/interactive-list-messages.md) |
| "Carousels and lists can be sent any time." | They are non-template messages. **Open window only** | [pricing](https://developers.facebook.com/documentation/business-messaging/whatsapp/pricing.md) |
| "Flows work everywhere." | **Android ≥6.0 and iOS ≥12 only. Not on WhatsApp Web or companion devices.** Always keep a conversational fallback | Flows overview |
| "Greeting and away messages are a WhatsApp feature we can switch on." | They are **WhatsApp Business *app*** features. On the Cloud API there is no native greeting or away message — you get ice breakers (first-open only) and whatever out-of-hours logic you write (inf.) | conversational-components, by omission |
| "Labels are a WhatsApp feature." | Also **app-only**. On Cloud API, tagging lives in your CRM or in Kapso contacts/assignments | inf. |
| "We can opt a guest back into marketing once they've resolved it with us." | **There is no API or dashboard control to opt a contact out or back in.** Only the contact can, inside WhatsApp, by tapping *Resume promotions* | [Kapso marketing-opt-outs](https://docs.kapso.ai/docs/whatsapp/templates/marketing-opt-outs) |
| "We can tell how many people scanned our QR code." | **No scan analytics exist**, by design. Use distinct prefilled messages per placement as your attribution | [qr-codes](https://developers.facebook.com/documentation/business-messaging/whatsapp/qr-codes.md) |
| "We can block a nuisance number." | Only if they messaged you **within the last 24 hours**. You also cannot block another WhatsApp Business account | [block-users](https://developers.facebook.com/documentation/business-messaging/whatsapp/block-users.md) |
| "The green tick is something you can buy or apply for directly." | OBA is a **blue** checkmark, and it requires a verified portfolio + approved display name + 2SV + 30 days registered. Rejection means a 30-day wait | [official-business-accounts](https://developers.facebook.com/documentation/business-messaging/whatsapp/official-business-accounts.md) |
| "Our number is findable in WhatsApp." | **Numbers without OBA do not appear in WhatsApp search results** | same |
| "Business verification gives us a badge." | It does not. It raises limits, unlocks Flows, and reduces ban risk (**secondary** — Chatfuel) | — |
| "Verification will take a day or two." | Usually 1–5 business days (**secondary**), but Meta's own community forum carries reports of multi-month "In Review" states. Never sequence a launch behind it | Meta community forum |
| "We can send a cart or an order to the guest." | **Businesses cannot send carts to customers.** Carts are per chat thread and per device, never expire, and cannot be edited once sent | [catalogs-overview](https://developers.facebook.com/documentation/business-messaging/whatsapp/catalogs/catalogs-overview.md) |
| "We'll put a booking link in a group chat." | Groups allow **no interactive messages** — no buttons, lists, CTA URL, carousels or Flows. Text, media and text/media templates only, ≤8 participants, OBA required | [groups](https://developers.facebook.com/documentation/business-messaging/whatsapp/groups.md) |
| "We can run marketing to any guest." | Not to **US** numbers (error 131049, since 1 Apr 2025), and all other markets are subject to an **adaptive, unpublished per-user cap** based on that user's read rate | [per-user-limits](https://developers.facebook.com/documentation/business-messaging/whatsapp/templates/marketing-templates/per-user-limits.md) |
| "A template asking for passport or card details is fine — guests send them anyway." | Requesting full payment-card numbers, financial account numbers, national ID numbers, **or documents likely to contain them** is an explicit rejection reason. Last-4 is allowed. Collect documents *inside* the window instead | [template-review](https://developers.facebook.com/documentation/business-messaging/whatsapp/templates/template-review) |
| "If Meta miscategorises our template we can always appeal." | Utility↔marketing, yes, within 60 days. **Reclassification to authentication is explicitly not appealable** — the template is set to `REJECTED` on the 1st of the following month | [template-categorization](https://developers.facebook.com/documentation/business-messaging/whatsapp/templates/template-categorization) |
| "A paused template just comes back." | Quality pauses auto-unpause (3 h → 6 h → **permanently disabled** on the third). But templates paused by **pacing** must be unpaused **manually** | [template-pausing](https://developers.facebook.com/documentation/business-messaging/whatsapp/templates/template-pausing.md) |
| "We'll switch from Kapso credits to our own Meta card later." | **Meta does not support switching a WABA off a partner shared credit line to a card**, even after the allocation is revoked. It requires a new WABA and a number migration | [Kapso billing](https://docs.kapso.ai/docs/whatsapp/meta-message-billing) |
| "Our messaging limit is our number's own." | **Since 7 Oct 2025 it is the business portfolio's**, shared by every number in it. One number can consume the whole portfolio's capacity | [upcoming-messaging-limits-changes](https://developers.facebook.com/documentation/business-messaging/whatsapp/upcoming-messaging-limits-changes.md) |

---

## 10. Kapso coverage summary — platform gap vs middleware gap

| Capability | Meta | Kapso exposes | Verdict |
|---|---|---|---|
| Templates (create, send, lifecycle, all sub-types) | ✅ | ✅ Platform API + Meta proxy | Available |
| Carousel templates | ✅ | ✅ via Meta proxy (`carousel.cards` forwarded untranslated) | Available |
| Free-form interactive carousel | ✅ | ✅ `sendInteractiveCarousel` | Available |
| Lists, buttons, CTA URL, location, location request, reactions, stickers, contacts, request-contact-info | ✅ | ✅ | Available |
| Flows (create, version, publish, data endpoint, encryption) | ✅ | ✅ Full | Available after verification |
| Product messages (single, list) | ✅ | ✅ | Available |
| Catalog upload / commerce settings / catalog templates | ✅ | ❌ | **Middleware gap** — Commerce Manager or Meta proxy |
| Broadcasts with per-recipient tracking + opt-out suppression | ❌ (Meta has no broadcast primitive) | ✅ | **Kapso adds value over Meta** |
| Marketing opt-out tracking & enforcement | ✅ webhook only | ✅ recorded, enforced, queryable, 422 before billing | **Kapso adds value over Meta** |
| Display name submit + statuses + rejection reasons | ✅ | ✅ (and documents the 24–48 h SLA Meta omits) | Available |
| Business usernames | ✅ | ✅ Meta proxy | Available |
| Business profile | ✅ | ✅ | Available |
| Block users | ✅ | ✅ | Available |
| Health status | ✅ | ✅ (3-min cache, own rate limits) | Available |
| Marketing Messages API | ✅ | ✅ `send-a-marketing-message` | Available after templates |
| Calling | ✅ | ✅ proxy + events; **you supply the media server** | Blocked by TIER_250 |
| Conversion events (CTWA attribution) | ✅ | ✅ | Available |
| **QR codes / short links** | ✅ | ❌ not documented | **Middleware gap** — WhatsApp Manager |
| **Ice breakers / commands** | ✅ | ❌ not documented | **Middleware gap** — WhatsApp Manager |
| **Groups API** | ✅ (OBA only) | ❌ not documented | **Middleware gap** + blocked by OBA |
| **CTWA welcome message sequences** | ✅ | ❌ not documented | **Middleware gap** |
| Greeting / away messages, labels | ❌ **platform gap** (app-only) | Kapso workflows / contacts / assignments | **Platform gap** — build it |
| WhatsApp Pay in Malaysia | ❌ **platform gap** | — | **Platform gap** — not solvable |

Kapso's `https://api.kapso.ai/meta/whatsapp/v24.0` base URL "mirrors Meta's Graph API shapes, so existing Cloud API code ports over with a base URL change" ([Kapso API intro](https://docs.kapso.ai/api/introduction)). The four middleware gaps above are **undocumented, not necessarily unsupported** — they may well pass through the proxy untouched (inf.). Worth one test call each before concluding anything is unavailable.

---

## 11. Open items to re-verify

1. **The 1,000 free service messages figure is not on Meta's own pricing page.** It is on Kapso's billing and pricing-FAQ pages and in a half-dozen vendor write-ups. Meta's `pricing.md` still contradicts the change outright. Re-check Meta's MYR rate card and pricing page directly, and confirm against the first real `pricing.type: regular, category: service` webhook Harper receives.
2. **Malaysia's published rates.** All figures here are vendor republications of Meta's MYR card (effective 1 Apr 2026). Download the MYR rate card from Meta's pricing page to confirm, especially whether the October card added a separate service row or genuinely reuses the utility rate.
3. **Whether the BUSINESS=LIMITED `additional_info` string names verification.** Query `health_status` on the BUSINESS node and read the actual text — Meta documents the model but exemplifies LIMITED only with the display-name case.
4. **The 6,000-template cap for verified portfolios** is vendor-reported; Meta's own page says 250 flatly. Not urgent at Harper's scale.
5. **Whether Kapso's Meta proxy passes `message_qrdls`, `conversational_automation` and `whatsapp_commerce_settings`.** One test call each.
6. **Commerce Policy and hotel/travel services.** Meta's own Commerce Policy page was not reachable in this audit; vendor copies are silent on travel. Check before building anything catalog-shaped.
7. **Meta's public changelog stops at 12 May 2026.** Anything between then and now is reconstructed from individual pages and Kapso. Re-read the changelog when it catches up.
