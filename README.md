# Hotel WhatsApp concierge — architecture and research

Research and system documentation from a working WhatsApp guest concierge for a
boutique hotel in Kota Kinabalu, Sabah. The bot answers guests in Malay, English
and Chinese, runs on the WhatsApp Business Platform through Kapso with a
Cloudflare Worker holding the logic, and calls a model only when no ready-made
reply fits.

The implementation is private. What is here is the part that is useful to anyone
else building one: what guests actually ask, what the commercial products in this
category do and don't do, what the WhatsApp platform allows, and what a hotel
line is supposed to earn.

## Contents

| | |
|---|---|
| [`architecture.html`](architecture.html) | The system as built, in five diagrams: system context, one turn through the workflow, the guard's decision order, how an answer is chosen, and where the replies come from. Open it in a browser — GitHub will not render it. |
| [`research/guest-questions.md`](research/guest-questions.md) | 89 questions a hotel guest actually sends, written without sight of the bot so it is a demand list rather than a mirror of what the bot already answers. Ranked by volume and by what a missing answer costs. Includes the Malaysian specifics a generic list misses — halal, surau, Grab, tourism tax, company invoices, durian. |
| [`research/market-chatbot-teardown.md`](research/market-chatbot-teardown.md) | HiJiffy, Asksuite, Quicktext, Duve, Whistle, Akia, Canary, Oaky and a dozen more: what ships as table stakes, what is premium, what hotels complain about after they buy, and what the published benchmarks are actually worth. |
| [`research/whatsapp-platform-gaps.md`](research/whatsapp-platform-gaps.md) | The WhatsApp Business Platform capability surface as of late 2026: templates, Flows, carousels, catalogues, payments, the calling API; the 24-hour window, the per-message pricing that replaced conversation pricing, messaging tiers, and business verification. |
| [`research/hotel-ops-gaps.md`](research/hotel-ops-gaps.md) | The guest lifecycle stage by stage, where a hotel line pays for itself, what a general manager asks about on day one, Malaysian PDPA and tourism tax obligations, and which metrics are worth measuring. |

## Three findings worth the click

**Nobody has independently measured hotel chatbot containment.** Every "we
automate 86% of conversations" figure in the category traces back to a vendor.
The only one with a stated denominator also reveals the volume behind it — 24
conversations per property per month — at which an 86% automation rate is about
twenty conversations, and will not displace a shift. The teardown names the
numbers that have a real numerator and denominator, and the ones that do not.

**Never quoting a price is an asset, not a limitation.** The only peer-reviewed
measurement of hotel chatbots (340 UK adults who had actually booked through
one) found inaccuracy drove booking abandonment at more than four times the next
factor, and named the failure modes: wrong room rates and misread cancellation
policies. A bot with no tool that can look up a price cannot make that mistake.

**The complaints are not about the AI.** Across review sites, hotelier forums
and trade press, what goes wrong after purchase clusters around the inbox nobody
watches, integrations shallower than sold, attribution that cannot be proven,
and pricing opacity — not answer quality, which is where both vendors and review
sites point.

## Method, and what to distrust

The research was produced by several agents working independently against
different sources, then merged and checked. Claims carry source URLs; anything
inferred rather than read is tagged `(inf.)`. Where sources conflict — and in
this category they conflict a lot, including inside a single vendor page — the
conflict is named rather than resolved silently.

Treat the vendor figures as what they are. The documents are explicit about
which numbers have a disclosed sample and method, which are marketing, and which
could not be verified at all.

## What is not here

The concierge implementation, its prompts and replies, the hotel's operational
identifiers, and the audit of the live system's own defects. Phone numbers and
account identifiers have been removed from these documents.
