---
name: platform-playbooks
description: Per-platform doctrine for distributing companion content (IG, X, TikTok, Snap, Threads, Reddit, bridge pages)
model: inherit
---

# Platform Playbooks Doctrine

How to think about each distribution surface and how they interlock into one funnel.

## The funnel architecture

```
[External platforms: TikTok, Snap, Threads] → [Instagram or X primary] → [Bridge page: Superlink] → [Fan platform profile] → [DM / chat] → [PPV monetization]
```

No single platform monetizes on its own. Instagram drives attention and followers, Twitter drives personality-based engagement, TikTok/Snap/Threads funnel traffic inward, the bridge page hides the monetization target from platform detection, and the fan platform (Fan View / analog) handles the subscription + chat + PPV transactions.

## Per-platform doctrine

### Instagram
- **Role:** primary attention surface and follower-base builder
- **Content mix:** reels (main reach driver) + carousels (saves/shares + portfolio impression) + stories (FOMO + close-friend feel)
- **Rhythm:** 1–3 posts/day, with at least one reel
- **Ban risk levers:** skin-exposure thresholds (#1 cause of bans per canvas.md), sexualized pose rules, metadata hygiene (sanitize SynthID / AI-content tags before upload)
- **Engagement:** outward comments on adjacent accounts of the same niche — reply-bait on ignored comments under bigger accounts, hook-hijacking top-performing reels in the niche
- **Verification:** worth getting even for AI companions (improves reach, signals legitimacy)
- **External traffic in:** loved by the algorithm — import from TikTok, Threads, Snap

### X / Twitter
- **Role:** personality-based engagement, quote-tweet virality, verified-account reach amplification
- **Content mix:** 80% text replies, 20% image replies under bigger niche accounts
- **Rhythm:** 1–3 posts + 50–100 replies/day (the replies are the lever — often handled by a VA)
- **Engagement:** rage-bait, hot-takes, niche commentary, quote-replies to trending accounts in the companion's passion axis
- **Ban risk:** lower than IG; X tolerates AI companions more; verified is cheap and high-ROI
- **Monetize via:** link in bio → bridge page

### TikTok / Snap / Threads
- **Role:** feeder platforms — funnel traffic into Instagram and X
- **Rhythm:** high-volume posting, low effort per post; batched from IG content
- **Reason:** IG's algo rewards external-traffic inflows, so consistent feeder activity boosts the primary surface

### Reddit
- **Role:** direct-to-fan-platform funnel (skip bridge page) for some niches
- **Caveat:** advanced — requires real Reddit-user persona or it will be flagged and banned
- **Avoid unless operator already understands Reddit**

### Bridge pages (Superlink / get-all-my-links)
- **Role:** hide the monetization target from platform detection
- **Why:** direct fan-platform links in IG/X bios get the account flagged
- **Implementation:** Superlink preferred (modern, low ban rate); get-all-my-links has reliability issues per canvas
- **Content:** one link in, multiple links out — subscribe, free preview, custom content request, latest story arc

### Fan platform (monetization surface)
- **Role:** where the money actually transacts — subscriptions, PPV DMs, tips, mass DMs
- **Per canvas.md:** Fan View is AI-companion-friendly (OnlyFans is not). Analogous platforms exist.
- **Setup requirements:** verified creator (KYC), profile photo, bio, banner, intro video, subscription price ($10–15 sweet spot), 25–50 feed images, 3–4 paid-feed posts at varied price points to identify whales, auto-DM configured

## Platform-platform interactions (how they compound)

- IG reel goes viral → follower spike → bridge page click-throughs spike → fan-platform sub spike → DM pipeline fills
- X quote-tweet goes viral → similar spike, faster cadence
- TikTok feeder posts push IG algo → IG reach compounds
- Snap/Threads funnel gets IG external-traffic boost
- A banned IG is survivable if X is strong — redundancy matters

## When to use this skill

- `/generate-niche` — pairing niches with platform fit
- `/build-companion` — selecting launch platforms
- `/performance-review` — evaluating per-platform ROI
- Troubleshooting a ban or a reach drop — reference the canonical platform node's ban-risk rules

## Relevant nodes
- `knowledge_base/platforms/` — one node per platform with current-cadence playbook
- `knowledge_base/tech-stack/` — tooling for posting, metadata-sanitization, phone ops
- `00_foundation/content-playbook/` — content patterns per platform

## Related commands
- `/build-companion` — launches default platform recommendations per companion
- `/draft-story-arc` — maps content across platforms per day
