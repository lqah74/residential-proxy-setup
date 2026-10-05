# dolphin anty proxy: How to Set Up Residential Proxies in Dolphin Anty and Pay Only for the Traffic You Use

Most Dolphin Anty problems don't come from the browser. They come from the IP address underneath it.

You can spend an afternoon tuning WebGL, canvas noise, fonts and audio fingerprints, get every profile to look like a separate device, then ruin all of it by running fifteen profiles through one datacenter IP. Platforms don't need to crack your fingerprint when the network layer gives you away in a single query. Dolphin Anty handles the device identity. Something else has to handle where that device appears to be sitting.

That's the whole job of a proxy in this setup, and it's why "dolphin anty proxy" searches usually come down to three practical questions: which proxy type actually survives platform checks, how to attach it without breaking the fingerprint, and what it costs per profile once you scale past a hobby account.

## The short answer on proxy type

Dolphin Anty accepts HTTP, SOCKS4, SOCKS5 and SSH proxies. It doesn't care which provider you buy from, and its own documentation is blunt about that: the browser does not regulate or take responsibility for how your proxies behave. If the proxy fails, you're talking to the proxy vendor, not the antidetect browser.

So the real filter is what the target platform sees:

- **Residential IPs** for anything involving account logins, marketplaces, social platforms or ad accounts. Real ISP-assigned addresses, historically cleaner than datacenter ranges.
- **Mobile IPs** when you're dealing with the most aggressive anti-fraud stacks, usually social apps and mobile-first marketplaces.
- **Datacenter IPs** for scraping, price checks, SERP monitoring — work where nobody is logging into an account and nobody cares that the IP belongs to a server farm.
- **Premium residential** when the standard pool isn't getting through and you want a filtered, higher-trust subset.

A cheap datacenter range attached to twenty marketplace accounts is the fastest way to burn a month of profile work. Speed isn't the constraint here. Trust is.

## Where the proxy layer sits in the stack

Dolphin Anty creates isolated browser environments. Each profile carries its own user-agent, WebGL signature, fonts, timezone, language and so on, and those values are deliberately aligned rather than randomized, because modern anti-fraud systems score the fingerprint as a whole rather than checking one signal.

The proxy handles the network origin. When the two agree — proxy geolocation matched to profile timezone, language and system settings — the profile reads as a coherent user. When they don't, you get a US IP with a Kyiv timezone and a Russian-language browser, which is a worse signal than no fingerprint spoofing at all.

DataImpulse is the provider most commonly slotted into this layer, largely because of how its billing works. It runs a first-party pool of 90M+ residential IPs across 195 countries, priced at $1 per GB on a pay-as-you-go basis with traffic that doesn't expire. For a multi-accounting workflow, the non-expiring part matters more than the headline rate: profile warm-ups are bursty, and prepaid monthly bundles get wasted during the weeks you're not running anything.

👉 [Check the current DataImpulse proxy plans and pricing](https://bit.ly/dataimPulse)

## Adding a DataImpulse proxy to a Dolphin Anty profile

The setup is genuinely short. Dolphin Anty supports several input formats, so you can paste credentials in whichever shape your dashboard gives them: `host:port`, `host:port:login:password`, or `login:password@host:port`, with the protocol prefixed when needed (`socks5://login:password@host:port`).

1. **Grab your endpoint from the DataImpulse dashboard.** You need the host, port, username and password for an endpoint. Pick the sticky-session port rather than the rotating one — more on that below.
2. **Open Dolphin Anty and create a new profile**, or edit an existing one.
3. **Find the proxy section** in the profile window and select **New Proxy**.
4. **Choose the connection type.** HTTP or SOCKS5 covers almost every DataImpulse endpoint. SOCKS4 and SSH are also supported if your workflow needs them.
5. **Paste the credentials.** Host, port, login, password. If you're pasting a single string, use one of the supported formats above and let the app parse it.
6. **Run the connection check.** Click the arrows on the right edge of the row. You'll get back connection status, detected geolocation and timezone.
7. **Fix the mismatch before saving.** If the proxy resolves to Frankfurt and your profile is set to New York, change the profile, not the proxy. Then hit **Create Profile**.

That last step is where most setups quietly fail. Dolphin Anty will happily run a profile with a timezone that contradicts its exit IP. Nothing errors out. The platform just notices.

## Rotating vs sticky: the setting that decides whether it works

A rotating proxy hands you a new IP on every request. That's ideal for bulk crawling and terrible for account work, because a marketplace session that changes country mid-checkout looks exactly like what it is.

For Dolphin Anty profiles you want **sticky sessions** — the same exit IP held for the length of the session. DataImpulse provides rotating endpoints as well as sticky-session ports with session lengths you can pin; third-party documentation of the platform describes sessions configurable from one minute up to two hours, with a 30-minute default when you don't specify anything. Confirm the exact port ranges in your own dashboard before you map ports to profiles, since that's the kind of detail providers do tweak.

There's a second option worth knowing if you're buying rotating traffic: Dolphin Anty has a **"Link to change IP"** field. Paste the rotation URL from your provider and an IP-change button appears on the profiles screen, so you can force a new exit on demand instead of waiting for the rotation timer. Useful for testing whether a bad IP or a bad profile is causing a block.

## Scaling past a handful of profiles

Adding proxies one at a time works fine for ten profiles. At two hundred it becomes a source of error, and the most common error is accidental IP reuse across profiles — the exact thing that breaks isolation and triggers platform reviews.

Dolphin Anty's built-in Proxy Manager stores your DataImpulse endpoints as a list and supports bulk import, so you can load a prepared pool in one go rather than typing credentials repeatedly. Once the list exists, profiles reference proxies from it instead of taking manual entries.

From there, bulk proxy assignment lets you distribute across multiple profiles at once. You can assign manually for precise control, randomly for a more natural spread, or by pattern — a new proxy to every Nth profile. Bulk proxy changes are gated behind Dolphin Anty's paid plans, so if you're still on the free tier, plan the manual route or budget for an upgrade.

Two other features are worth flagging because they change your traffic math. Profile automation can sync repetitive actions across many profiles, and the built-in cookie robot collects cookies in the background without loading full pages — which keeps proxy traffic lower during warm-up. If you're paying per GB, the cookie robot is effectively a discount on every profile you're ageing.

## What this actually costs

Here's the full DataImpulse plan structure. Every product line uses the same pay-as-you-go logic: no subscription, no monthly reset, purchased traffic doesn't expire. The $5 you spend on any Intro plan is the minimum top-up, and it buys different amounts depending on the proxy type.

| Proxy type | Plan | Traffic included | Price | Per GB | Billing | Get it |
| --- | --- | --- | --- | --- | --- | --- |
| Residential | Intro | 5 GB | $5 | $1.00 | Pay-as-you-go, no expiry | [Get the Residential Intro plan](https://bit.ly/dataimPulse) |
| Residential | Basic | 50 GB | $50 | $1.00 | Pay-as-you-go, no expiry | [Get the Residential Basic plan](https://bit.ly/dataimPulse) |
| Residential | Advanced | 1 TB | $800 | $0.80 | Pay-as-you-go, 20% volume discount | [Get the Residential Advanced plan](https://bit.ly/dataimPulse) |
| Residential | Custom+ | 5 TB+ | Custom quote | Custom | Enterprise, personalized features | [Request a Residential Custom+ quote](https://bit.ly/dataimPulse) |
| Datacenter | Intro | 10 GB | $5 | $0.50 | Pay-as-you-go, no expiry | [Get the Datacenter Intro plan](https://bit.ly/dataimPulse) |
| Datacenter | Basic | 100 GB | $50 | $0.50 | Pay-as-you-go, no expiry | [Get the Datacenter Basic plan](https://bit.ly/dataimPulse) |
| Datacenter | Advanced | 1 TB | $450 | $0.45 | Pay-as-you-go, volume discount | [Get the Datacenter Advanced plan](https://bit.ly/dataimPulse) |
| Datacenter | Custom+ | 5 TB+ | Custom quote | Custom | Enterprise scale | [Request a Datacenter Custom+ quote](https://bit.ly/dataimPulse) |
| Mobile | Intro | 2.5 GB | $5 | $2.00 | Pay-as-you-go, no expiry | [Get the Mobile Intro plan](https://bit.ly/dataimPulse) |
| Mobile | Basic | 25 GB | $50 | $2.00 | Pay-as-you-go, no expiry | [Get the Mobile Basic plan](https://bit.ly/dataimPulse) |
| Mobile | Advanced | 1 TB | $1,600 | $1.60 | Pay-as-you-go, 20% volume discount | [Get the Mobile Advanced plan](https://bit.ly/dataimPulse) |
| Mobile | Custom+ | 5 TB+ | Custom quote | Custom | Enterprise, personalized features | [Request a Mobile Custom+ quote](https://bit.ly/dataimPulse) |
| Premium Residential | Intro | 1 GB | $5 | $5.00 | Pay-as-you-go, no expiry | [Get the Premium Residential Intro plan](https://dataimpulse.com/premium-residential-proxies/?aff=86938) |
| Premium Residential | Basic | 10 GB | $50 | $5.00 | Pay-as-you-go, no expiry | [Get the Premium Residential Basic plan](https://dataimpulse.com/premium-residential-proxies/?aff=86938) |
| Premium Residential | Custom+ | 5 TB+ | Custom quote | Custom | Dedicated account manager, all targeting included | [Request a Premium Residential quote](https://dataimpulse.com/premium-residential-proxies/?aff=86938) |

A few conditions sit behind those numbers, and they matter for planning:

- **Country targeting is included in the base price.** Advanced filters — state, city, ZIP and specific ASN selection — are billed at double the standard residential per-GB rate on residential plans, per third-party breakdowns of the platform. Datacenter plans advertise those same filters as included. Verify the current billing treatment in your dashboard before you build a city-targeted workflow into a budget.
- **The 20% volume discount kicks in at 1 TB** on residential and mobile. Below that, the per-GB rate is flat, which is why the Intro and Basic tiers cost the same per gigabyte.
- **Intro plans carry a 7-day money-back guarantee** on card payments, provided less than 80% of the traffic has been consumed. Crypto purchases aren't refundable. There's no free trial, so the $5 Intro plan is the de facto trial.
- **DataImpulse advertises a 4.8/5 rating on G2** and states that its residential pool is first-party rather than resold, which is the claim behind its lower block rates on protected sites.

## Which tier fits which setup

Editorial judgment, based on what the numbers above actually buy you:

**Five to ten profiles, light browsing.** Residential Intro at $5 for 5 GB. Five gigabytes disappears faster than you'd think on a JS-heavy e-commerce site, but for warming up a handful of profiles it's enough to find out whether residential IPs fix your problem at all.

**Twenty to fifty profiles with real activity.** Residential Basic at $50 for 50 GB. This is the tier most people settle on, because it stops per-gigabyte cost from affecting per-profile decisions.

**Operations running at scale.** Residential Advanced at $800 for 1 TB, which drops you to $0.80/GB. Only worth it once you're genuinely pushing toward a terabyte — the discount is the reason to be there, not the tier name.

**Platforms that reject residential outright.** Mobile at $2/GB. Expect to pay roughly double for the same volume, and don't buy it "just in case".

**Accounts where a single block is expensive.** Premium Residential at $5/GB, where the pitch is a filtered higher-trust pool, all targeting options included, and a dedicated account manager. Five times the residential rate is a hard number to justify for scraping. For an ad account that generates revenue, it's easier arithmetic.

Datacenter is the odd one out in a Dolphin Anty context: at $0.50/GB it's the cheapest thing on the page, and it's the wrong choice for logged-in accounts. Buy it for the scraping side of your workflow, not for the profiles.

👉 [Compare all DataImpulse proxy types on one page](https://bit.ly/dataimPulse)

## Mistakes that waste the most money

**One proxy shared across profiles.** Isolation breaks the moment two profiles exit through the same address. If you take nothing else from this article, take the bulk-assignment habit of distributing proxies deliberately rather than reusing your first three endpoints.

**Timezone and geolocation drift.** Match the profile to the IP, not the reverse. Dolphin Anty shows you both after the connection check — use that reading.

**Datacenter IPs on marketplace accounts.** Cheapest per gigabyte, most expensive in the long run.

**Ignoring the cookie robot's traffic.** Background cookie collection still burns bandwidth. If you're measuring cost per profile, include it.

**Expecting Dolphin Anty to fix proxy failures.** Its documentation says plainly that the browser doesn't manage or take responsibility for proxy connections, and that support issues belong with the vendor. Twenty minutes in your dashboard beats an afternoon in a support queue.

If the port mapping or a specific targeting question is unclear, DataImpulse's own walkthrough of the Dolphin Anty pairing covers the flow in detail, including the bulk import path.

👉 [Read the DataImpulse guide to using Dolphin Anty with its proxies](https://dataimpulse.com/blog/how-to-use-dolphin-anty-with-dataimpulse-proxies/?aff=86938)

## Questions that come up before buying

**Does Dolphin Anty include free proxies?** The app has a "Get free proxies" button that connects partner services, each with a small free traffic allowance tied to your Dolphin Anty plan. Those allowances are measured in a few gigabytes at most and are meant for testing. If your provider of choice isn't the one listed in that window, you add it manually through the same proxy form described above — same result, no integration required.

**Can one proxy cover several profiles?** Not if you want the profiles kept apart. The IP is the layer that ties them together, and reusing it undoes the fingerprint work.

**Do I need SOCKS5 specifically?** Both HTTP and SOCKS5 are supported by Dolphin Anty and by DataImpulse. What matters more is whether your endpoint is sticky or rotating, and whether the protocol matches what you configured in the dashboard.

**Does the traffic I buy ever expire?** No. Purchased gigabytes sit in the account until you use them, across every tier listed above. That's the main structural difference from subscription-based providers, and it's the reason a $5 top-up can sit dormant for months between warm-up pushes.

**What's the minimum spend?** $5, on any product line. That buys 5 GB of residential, 10 GB of datacenter, 2.5 GB of mobile or 1 GB of premium residential.

The setup itself is a ten-minute job. Getting the proxy type, session mode and geolocation alignment right is what decides whether twenty profiles survive the month — and at $1 per gigabyte with no monthly clock running, testing that properly costs about as much as a coffee.
