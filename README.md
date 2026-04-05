# Looking Glass KVM: Test Before You Commit, Route Before You Rent

Before you click "buy" on a VPS, there's a smarter move — one most newcomers skip and most veterans swear by. It's called Looking Glass, and if you're shopping for a KVM VPS with decent network performance, it's the single most useful pre-purchase test you can run.

Here's how it actually works, and why BandwagonHost's network of Looking Glass tools is one of the best free resources in the hosting world.

---

## What Is a Looking Glass, Exactly?

Think of a Looking Glass as a window into a datacenter's network, opened from the outside.

A Looking Glass is an open-source publicly available networking script that lets you check the host, ping, traceroute, MTR, speed, and latency of a VPS server and its network from a remote location. Instead of testing from your own machine (which only tells you the outbound path), a Looking Glass flips the script — it runs network tests *from the datacenter's servers* toward your IP address.

Looking Glass lets users remotely test VPS latency from different data centers to help them choose the best server. When testing network latency, users can run commands like ping and traceroute directly from the data center, giving them an idea of the speed and stability of the connections between their location and the VPS.

In practical terms: you enter your IP, pick a test (ping, traceroute, or MTR), and the datacenter runs it toward you. The result shows the *return route* — which is almost always more informative than your outbound route, because congestion almost always happens on the return leg.

The Ping command measures round-trip time and packet loss. Traceroute identifies the routers that facilitate access from the remote network to a given Internet resource and measures the round-trip delay of data packets to each hop. MTR combines the features of both traceroute and ping into a single network diagnostic utility.

---

## Why KVM Makes the Looking Glass Results Actually Meaningful

Not all VPS virtualizations are equal when it comes to network testing. Container-based solutions like OpenVZ share the host kernel, which means network resources — and their measurement — get muddied across tenants.

KVM is different. KVM virtualization provides full virtualization rather than container-based solutions, meaning better isolation between VPS instances and more consistent performance. You're not sharing kernel resources with hundreds of other users — each VPS operates as an independent virtual machine.

This matters for Looking Glass testing because the results you see from a KVM datacenter reflect *genuine network conditions* rather than a noisy average of shared resources. When a Looking Glass node on a KVM infrastructure shows you 158ms average latency with zero packet loss, that's the number you're actually going to experience.

---

## Scenario 1: You Want to Serve an Audience in China

This is the most common scenario where people turn to Looking Glass testing. China's network is complex — three major carriers (China Telecom, China Unicom, China Mobile), each with its own routing behavior, congestion patterns, and peak-hour variability.

The problem: you can't know which route a datacenter uses until you test. Marketing pages say "optimized for China" — but optimized how? CN2 GT? CN2 GIA? Plain ChinaNet?

CN2 GIA is the most expensive way to transfer data to/from China. Although, over the years, it has shown the least amount of problems — it is very stable. This is the network you want to use for a web conference, VOIP, serving web content, online gaming, as it will provide the best stability.

BandwagonHost provides dedicated Looking Glass tools for each datacenter, so you can test the actual return route to your Chinese IP before purchasing anything. If the traceroute output from DC9 shows AS4809 hops on the return path, you're on CN2 GIA. If it shows AS4134 (ChinaNet), it's the congested public route. Traceroute tests the return route — this is the one that actually matters. The traceroute output clearly shows each hop's IP, AS number, IP location, and latency information, making it easy to confirm whether the path uses CN2 GIA routing.

BandwagonHost's Looking Glass nodes for this use case:

- **DC9 (USCA_9) — Los Angeles CN2 GIA**: `dc9.52bwg.com` — USCA_9 offers the best overall network capacity and stability. All China-bound traffic is sent to three carriers: CN2 GIA by China Telecom (AS4809), CMIN2 (China Mobile AS58807) and China Unicom Premium (AS10099).
- **DC6 (USCA_6) — Los Angeles CN2 GIA-E**: `dc6.52bwg.com`
- **HK85 — Hong Kong**: `hk85.52bwg.com`
- **JPOS_1 — Japan Osaka Softbank**: `jpos.52bwg.com`
- **EUNL_9 — Amsterdam**: `eunl9.52bwg.com`
- **USCA_FMT8 — Fremont**: `fmt8.52bwg.com`

Each tool lets you run ping, MTR, and traceroute. For the China routing check, traceroute is your best friend — look for AS4809 in the output.

👉 [Browse BandwagonHost's CN2 GIA plans to match your test results](https://bwh81.net/aff.php?aff=77528)

---

## Scenario 2: You Need to Compare Multiple Datacenters Before Committing

Maybe you're not sure whether Los Angeles or Tokyo will serve your users better. Or whether you need to pay for Hong Kong or if Singapore is close enough. This is exactly what Looking Glass was built for.

The workflow is simple:

1. Note your own public IP address (use any "what is my IP" site)
2. Visit each datacenter's Looking Glass tool
3. Enter your IP and run MTR
4. Compare the average latency and packet loss columns

Since network latency can vary, run multiple ping tests to ensure all is well. Record the average network latency time to get a basic idea of how quickly the network responds between the selected server and your location.

BandwagonHost makes this particularly useful because their KVM VPS plans include **free datacenter migration via the KiwiVM control panel**. The datacenter migration feature deserves special attention. You can buy a Los Angeles VPS, realize Tokyo works better for your needs, then just migrate. No setup fees, no waiting days, no buying a new server. It's a few clicks and about five minutes of downtime.

But even with that flexibility, starting in the right datacenter saves you the hassle. The Looking Glass test takes five minutes. The migration, while easy, still involves downtime and a learning curve. Test first.

---

## Scenario 3: You're Troubleshooting an Existing VPS

You bought the plan, the server is running, but something feels off — pages load slowly in the evenings, SSH sessions are laggy, your users in a particular region are complaining.

Looking Glass is still the right tool. Run an MTR from the datacenter toward your home IP or a representative user's IP. Look at:

- **Loss%** — anything above 1–2% at any hop is a red flag
- **Avg latency per hop** — large jumps between adjacent hops indicate congestion
- **The AS numbers** — if you're supposed to be on CN2 GIA but see AS4134 hops in the middle, something's wrong with routing

Comprehensive test results give users detailed insights into the number of hops, round-trip time, and potential delays, enabling them to determine the efficiency of the network and identify the best route for data transmission. Looking Glass can be used to optimize routing paths, improve speed and reliability for end users.

If you're on BandwagonHost's CN2 GIA-E plan and the traceroute from DC9 shows clean routing with consistent latency, the bottleneck is likely elsewhere (your ISP's last mile, the CDN, your application). If it shows degraded paths, you can migrate datacenters with one click in KiwiVM.

---

## Scenario 4: You're Running Applications That Are Latency-Sensitive

Online gaming, VoIP, live streaming — for these, a 50ms difference can be the gap between smooth and broken.

The Looking Glass ping test gives you baseline RTT. But for latency-sensitive workloads, you want MTR, not just ping.

MTR combines the features of both traceroute and ping, and investigates the network connection between the host and the destination. MTR prints the response percentage and response times of the internet route to the target, including statistics on packet loss and average delays at each hop.

For latency-sensitive use cases, look for:
- RTT under 100ms (if your users are within the same region)
- Zero packet loss across all hops
- No large latency "jumps" between specific hops that would indicate transatlantic segments you didn't expect

BandwagonHost's Hong Kong and Japan nodes are specifically designed for this scenario — geographically close to mainland China and much of Southeast Asia, running CN2 GIA or Softbank direct routes. Hong Kong and Japan based CN2 GIA VPS plans cost more, but the network quality justifies the price for latency-sensitive applications.

👉 [Check Hong Kong and Japan CN2 GIA plan availability](https://bwh81.net/aff.php?aff=77528)

---

## How to Actually Use the BandwagonHost Looking Glass

Here's the quick-start guide, no fluff:

1. **Go to the Looking Glass URL** for the datacenter you want to test (e.g., `dc9.52bwg.com/lookingglass/indexen.php`)
2. **Enter your IP address** — the page often auto-detects it and shows a "Your IP" button
3. **Select your test type**:
   - **Ping** — fast, good for baseline latency
   - **Traceroute** — shows the full hop-by-hop path, great for confirming route quality (CN2 GIA vs. regular)
   - **MTR** — combines both, shows packet loss per hop, best for thorough diagnosis
4. **Click "Run Test"** and wait ~10–30 seconds for results
5. **Read the output**:
   - Look for AS4809 in traceroute = CN2 GIA
   - Look for AS4134 = ChinaNet (congested public route)
   - Look for AS58807 = CMIN2 (China Mobile's premium route)

Run the same test from multiple datacenter Looking Glass pages to compare. The one with the lowest latency and cleanest packet loss percentage to your location is where you want your VPS.

---

## BandwagonHost KVM VPS Plans — Full Comparison

All plans run on KVM virtualization with the KiwiVM control panel. BandwagonHost includes free snapshots, no overage charges (bandwidth-exceeded VPS gets suspended until next month, not charged), and supports Alipay, PayPal, credit card, and UnionPay.

**Current promo code: `BWHCGLUKKB` — 6.77% recurring discount, applies to renewals too.**

### Standard KVM Plans (Basic Routing — CN2 GT / Multi-Location)

| Plan | RAM | Storage | Transfer | Price | Purchase |
|------|-----|---------|----------|-------|----------|
| 20G KVM | 1 GB | 20 GB SSD RAID-10 | 1 TB/mo | $49.99/yr |  [Get this plan](https://bwh81.net/aff.php?aff=77528&gid=1) |
| 40G KVM | 2 GB | 40 GB SSD RAID-10 | 2 TB/mo | $52.99/6mo |  [Get this plan](https://bwh81.net/aff.php?aff=77528&gid=2) |
| 80G KVM | 4 GB | 80 GB SSD RAID-10 | 3 TB/mo | $19.99/mo |  [Get this plan](https://bwh81.net/aff.php?aff=77528&gid=3) |
| 160G KVM | 8 GB | 160 GB SSD RAID-10 | 4 TB/mo | $39.99/mo |  [Get this plan](https://bwh81.net/aff.php?aff=77528&gid=4) |
| 320G KVM | 16 GB | 320 GB SSD RAID-10 | 5 TB/mo | $79.99/mo |  [Get this plan](https://bwh81.net/aff.php?aff=77528&gid=5) |
| 480G KVM | 24 GB | 480 GB SSD RAID-10 | 6 TB/mo | $119.99/mo |  [Get this plan](https://bwh81.net/aff.php?aff=77528&gid=6) |

*Available datacenters: Los Angeles (DC2/DC3/DC4/DC8), Fremont, New York, New Jersey, Vancouver, Amsterdam*

### CN2 GIA-E Plans (Premium Routing — Triple-Network Optimized)

These plans support migration across 13+ datacenters, including DC6, DC9, Japan Softbank, Netherlands, Singapore, and more.

| Plan | RAM | Storage | Transfer | Price | Purchase |
|------|-----|---------|----------|-------|----------|
| CN2 GIA-E Basic | 1 GB | 20 GB SSD | 1 TB/mo | ~$49.99/qtr |  [Get this plan](https://bwh81.net/aff.php?aff=77528&gid=11) |
| CN2 GIA-E Standard | 2 GB | 40 GB SSD | 2 TB/mo | $169.99/yr |  [Get this plan](https://bwh81.net/aff.php?aff=77528&gid=12) |
| CN2 GIA-E Plus | 4 GB | 80 GB SSD | 3 TB/mo | Higher tier |  [Browse all tiers](https://bwh81.net/aff.php?aff=77528) |

*Network: China Telecom CN2 GIA + China Mobile CMIN2 + China Unicom 9929 — all three carriers, all premium routes*

### Hong Kong CN2 GIA Plans (Lowest Latency to Mainland China)

| Plan | RAM | Storage | Transfer | Price | Purchase |
|------|-----|---------|----------|-------|----------|
| HK Basic | 2 GB | 40 GB SSD | 500 GB/mo | $46.70/qtr (~$15.57/mo) |  [Get this plan](https://bwh81.net/aff.php?aff=77528&gid=22) |
| HK Standard | 4 GB | 80 GB SSD | 1 TB/mo | Higher tier |  [Browse HK plans](https://bwh81.net/aff.php?aff=77528) |
| HK Premium | Higher configs | Up to 160 GB | Higher | Up to $899.99/yr |  [Browse HK plans](https://bwh81.net/aff.php?aff=77528) |

*Datacenter: Equinix HK2 (HK8) — NVMe RAID-10 SSD, AMD EPYC processors*

### Japan & Other Regional Plans

| Plan | Location | RAM | Storage | Price | Purchase |
|------|----------|-----|---------|-------|----------|
| Tokyo CN2 GIA Basic | Tokyo, JP | 2 GB | 40 GB SSD | $49.99/mo |  [Get this plan](https://bwh81.net/aff.php?aff=77528&gid=31) |
| Osaka Softbank | Osaka, JP | Configurable | Various | Various |  [Browse Japan plans](https://bwh81.net/aff.php?aff=77528) |
| Dubai (AEDXB_1) | UAE | 1 GB+ | 20 GB+ | From $49.99/qtr |  [Browse Dubai plans](https://bwh81.net/aff.php?aff=77528) |
| Sydney Limited | Australia | Various | Various | $99.99/yr (limited) |  [Check availability](https://bwh81.net/aff.php?aff=77528) |
| Vancouver | Canada | Various | NVMe | Various |  [Browse CA plans](https://bwh81.net/aff.php?aff=77528) |

---

## Matching Your Looking Glass Test to the Right Plan

After you've run your tests, here's the decision framework:

**You saw low latency (sub-150ms) from DC9 and clean CN2 GIA routing** → Go with a CN2 GIA-E plan on DC9 (USCA_9). This is the most popular choice for users who need reliable China connectivity at a reasonable price.

**You saw better latency from HK85 (Hong Kong)** → Your audience is close to mainland China. The Hong Kong CN2 GIA plans are worth the premium. Single-digit milliseconds to Chinese cities is genuinely rare and valuable.

**You don't need China-specific routing, just want reliable cheap KVM** → Standard plans at $49.99/year are an exceptional deal. Six datacenter choices, KVM virtualization, RAID-10 SSD, and KiwiVM — it's hard to beat at this price.

**You're in the Middle East or testing from a Dubai IP** → The Dubai AEDXB_1 datacenter exists exactly for you.

👉 [Start with BandwagonHost's plan selector](https://bwh81.net/aff.php?aff=77528)

---

## A Few Things Worth Knowing Before You Buy

**On bandwidth:** When you're out of bandwidth, you won't incur any overage charges. Instead, your VPS will be automatically suspended until the end of the month. This is actually a good thing — predictable costs, no surprise bills.

**On payment:** BandwagonHost does not charge automatically. You pay manually each billing cycle, which means you're in control.

**On datacenter migration:** Any CN2 GIA-E plan lets you migrate freely between 13+ datacenters directly from the KiwiVM panel. This is a huge deal — it means your Looking Glass test today doesn't lock you in forever. Try LA first, migrate to Tokyo next month if the routing looks better. No cost, minimal downtime.

**On hardware:** Recent updates include AMD EPYC servers with NVMe RAID-10 storage in Hong Kong (HK3 and HK8) and Los Angeles DC9 (USCA_9), as well as AMD High-frequency CPUs with NVMe storage in Vancouver. The hardware has been getting notably better across the premium locations.

**On the promo code:** `BWHCGLUKKB` gives a 6.77% recurring discount — meaning it applies to every renewal, not just the first payment. Over a year on even a mid-tier plan, that adds up.

---

## The Short Version

If you're choosing a KVM VPS and you care even slightly about network performance — especially to Asia or China — run a Looking Glass test before you buy. It takes five minutes and shows you exactly what you're getting.

BandwagonHost provides Looking Glass tools for every major datacenter they operate: DC9, DC6, Hong Kong, Japan Osaka, Amsterdam, Fremont, and more. The results you see are genuine KVM-grade network performance, not averaged-out container noise.

Test the route. Confirm the AS numbers. Buy the plan that matches what you need.

👉 [Explore BandwagonHost KVM VPS plans](https://bwh81.net/aff.php?aff=77528)
