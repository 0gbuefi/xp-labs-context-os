---
name: EMAIL_WATERFALL_3_4_PROVIDERS
description: Waterfall 3-4 email finding providers maximum - diminishing returns after that due to catch-all domains
scope: agency
domain: list-building
node_type: pattern
status: emergent
created: 2026-01-15
last_updated: 2026-01-15
tags:
  - list-building
topics:
  - enrichment-tactics
  - verification-methods
  - data-sourcing
related_concepts:
  - "[[catch-all-domain-problem]]"
  - "[[double-verification-strategy]]"
  - "[[data-provider-tools]]"
source: "GEX Wrapped 2024 by Eric Nowoslawski"
source_url: ""
date_accessed: 2026-01-15
---

# Email Waterfall: 3-4 Providers Maximum

Waterfall **3-4 email finding providers** maximum, then stop. Adding more providers yields diminishing returns because catch-all domains can't be verified - you'll pay multiple providers for undeliverable emails.

## Core Principles

- No single provider has 100% email coverage
- Waterfall = if provider 1 fails, try provider 2, then 3, then 4
- Catch-all domains can't be validated by standard methods
- After 4 providers, you're mostly paying for catch-alls (wasted cost)
- Quality over coverage - focus on verified emails

## When to Use

Use 3-4 provider waterfall when:
- Building lists in Clay or similar automation tool
- Maximizing email coverage for high-value prospects
- Working with limited TAM (need maximum coverage)
- Budget allows for multiple data provider credits
- Final verification step removes catch-alls

## How to Apply

**Recommended Waterfall Structure:**

**Provider 1:** Prospeo / LeadMagic / TryKitt / IcyPeas
**Provider 2:** Different provider from list above
**Provider 3:** Third provider from list above
**Provider 4:** Instantly email validation (catches historically verified emails)

**Logic:**
```
IF provider_1.email_found AND email_valid:
    use_email()
    stop_waterfall()
ELSE IF provider_2.email_found AND email_valid:
    use_email()
    stop_waterfall()
ELSE IF provider_3.email_found AND email_valid:
    use_email()
    stop_waterfall()
ELSE IF provider_4.email_found AND email_valid:
    use_email()
    stop_waterfall()
ELSE:
    mark_as_no_email_found()
```

**Why Stop at 4:**

**Catch-all domain problem:**
- Catch-all domains accept all emails (real or fake)
- Standard validation can't confirm specific email exists
- Providers 5-8 will find "emails" on catch-alls
- You pay each provider for the same invalid email
- Catch-all verification tools exist but increase bounce rate

**Example:**
- You want: [email protected]
- Domain: examplecompany.com is catch-all
- Provider 1: "Valid" ✓ (but is it?)
- Provider 2: "Valid" ✓ (same result)
- Provider 3: "Valid" ✓ (same result)
- **Reality:** All three providers pass syntax/DNS/MX checks, but can't SMTP verify because it's catch-all

**GEX Waterfall:**
1. Kitt
2. LeadMagic
3. Prospeo
4. Instantly validation (uses historical send data)
5. **STOP**

**Cost Optimization:**

Providers charge per lookup (even failures). Adding 8 providers:
- Increases cost by 8x for marginal gains
- Mostly finds catch-alls (undeliverable)
- ROI negative after provider 4

**Alternative - Targeted Coverage:**

Instead of 8-provider waterfall, use:
- 3 email providers
- 1 verification service
- Manual research for VIP prospects

**Double Verification Protocol:**

After waterfall, verify all emails:
1. **Primary verification:** Debounce / MillionVerifier / Reoon
2. **Secondary verification:** Instantly (historical send data)

This catches emails that pass provider checks but are actually invalid.

## Evidence

[VERIFIED: GEX Wrapped 2024] "In 2024, the 'email waterfall' became more popular. The basic idea is that not one provider could be trusted for email verification so if one doesn't get a valid email, try another. We will waterfall 3-4 email providers and no more than that to optimize for cost and operational efficiency."

[DATA: Catch-all problem] "Catch All email addresses are the reason to not waterfall 8 different providers. As I explained above, a catch all email address cannot be validated by normal validation methods. So if the domain isn't possible to be validated, you could end up paying multiple data providers to never really get you a safe to send email."

[VERIFIED: Provider trust] "We trust providers like Kitt, Lead Magic, and Prospeo to do the catch all validation. Double check with Instantly's email validation and then end our waterfall."

[DATA: Diminishing returns] "I have found that yes, adding more providers will get you slightly better coverage but you get diminishing returns on cost since you're paying each provider for those catch all emails found."

## Related Concepts

- [[catch-all-domain-problem]] - Why catch-alls prevent effective verification
- [[double-verification-strategy]] - Post-waterfall verification protocol
- [[data-provider-tools]] - Specific recommended email finding tools
