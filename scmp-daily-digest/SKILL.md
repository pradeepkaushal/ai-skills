---
name: scmp-daily-digest
description: Fetch and summarize the day's news from the South China Morning Post (scmp.com) into a dated markdown digest covering nine sections — Latest, China, Economy, Hong Kong, Asia, Business, Tech, World, and Opinion. The digest closes with two analysis sections written for an Indian tech reader: "China moves India hasn't matched yet" and "AI monetization opportunities for India". Use this skill whenever the user asks for the SCMP digest, the daily China news summary, the South China Morning Post roundup, their "morning china post", what's happening in China / Hong Kong / Asia today, or wants China-vs-India gap analysis or AI business ideas drawn from today's Chinese and Asian tech news. Triggers on phrases like "scmp digest", "china news summary", "morning china post", "what's in scmp today", "daily asia roundup", "china tech opportunities" — even if the user never says the word "skill".
---

# SCMP Daily Digest

Turn the day's South China Morning Post coverage into one dated markdown file the user can read in a few minutes and act on. The reader is an India-based software engineer / would-be founder, so the digest does two things a plain news summary doesn't: it flags where **China is ahead of India**, and it surfaces **AI product ideas buildable for the Indian market**.

This skill reads public news pages and writes a local file. It does not post anything anywhere.

## Workflow

1. **Get today's date** (`date +%Y-%m-%d`). Use it for the filename and the digest header.
2. **Fetch all nine section pages** — see URLs below. Fire the `WebFetch` calls in parallel; they are independent.
3. **Smart-scan for depth** — after you have the headlines, pick the 4-8 most consequential stories and `WebFetch` their article URLs to get fuller detail. SCMP is metered: some articles return only a teaser. Work with whatever loads — never invent body text.
4. **Synthesize** the digest using the template below.
5. **Write the two analysis sections** — this is the part the user actually came for. Take real time here.
6. **Save** to `scmp-digest/<YYYY-MM-DD>.md` in the current working directory (create the folder if missing). If the user named a different path, use that. Then tell the user the path and give them a 3-5 line spoken summary of the highlights.

## Section pages

Fetch each of these. "Latest" feeds the **Top Stories** block; the other eight each get a **Section Brief**.

| Section    | URL |
|------------|-----|
| Latest     | https://www.scmp.com/ |
| China      | https://www.scmp.com/news/china |
| Economy    | https://www.scmp.com/economy |
| Hong Kong  | https://www.scmp.com/news/hong-kong |
| Asia       | https://www.scmp.com/news/asia |
| Business   | https://www.scmp.com/business |
| Tech       | https://www.scmp.com/tech |
| World      | https://www.scmp.com/news/world |
| Opinion    | https://www.scmp.com/comment/opinion |

**WebFetch prompt to use for a section page** — ask for extraction, not summary:

> "List every news article visible on this page. For each one give: the exact headline, the standfirst/summary blurb if present, and the article URL. Preserve the order shown. Do not summarize, merge, or skip articles."

If a page returns thin or no content (paywall wall, JS-only render), retry once. If it still fails, note that section as "could not load" in the digest rather than guessing — an honest gap is more useful than fabricated news.

## Handling overlap and recency

- The same story often appears under Latest, China, and Tech. **Deduplicate**: each story appears once, in its most natural section, and is not repeated.
- Section pages mix today's articles with ones a day or two old. Favor items that read as current. Where a date is visible and a story is clearly older, either drop it or label it "(earlier this week)". Don't claim everything is from "today" when you can't tell.

## Digest template

Use this structure exactly:

```markdown
# SCMP Daily Digest — <YYYY-MM-DD>

> Source: South China Morning Post (scmp.com) · Generated <timestamp>

## Top Stories Today
<3-6 of the most significant items across all sections, one line each, with link>

## Section Briefs

### China
- **<Headline>** — <1-2 sentence summary in your own words.> [link]
...

### Economy
...
### Hong Kong
...
### Asia
...
### Business
...
### Tech
...
### World
...
### Opinion
- **<Headline>** — <the author's core argument in 1-2 sentences.> [link]
...

## 🇨🇳 China Moves India Hasn't Matched Yet
<see guidance below>

## 🤖 AI Monetization Opportunities for India
<see guidance below>
```

Aim for roughly 4-8 bullets per section brief — enough to be representative, not a full dump. Summaries are your own words, never copied sentences.

## The two analysis sections — do these well

These are the point of the skill. A generic news summary is everywhere; this framing is not. Reason from the actual stories you fetched — don't pattern-match on keywords.

### 🇨🇳 China Moves India Hasn't Matched Yet

The reader wants to know: *what is China doing that I should be aware of because India is behind, smaller, or absent here?*

Pick stories that describe a **concrete capability, deployment, policy, product, or infrastructure milestone** — a chip advance, a digital-yuan feature, a drone-delivery rollout, a high-speed-rail or grid milestone, an industrial-policy move, an EV or battery development. Skip pure geopolitics, scandal, and personnel news; they don't represent a gap to act on.

For each item (target 3-6; fewer is fine — say so if today is quiet):

- **What China did** — the development, in one or two sentences.
- **Where India stands** — is there an Indian equivalent? At what scale or stage? If you're not confident, use `WebSearch` to check before claiming a gap. If India actually has something comparable, either drop the item or state the nuance honestly — a miscalled "gap" destroys the reader's trust.
- **Why it matters** — what the gap implies for India: an opportunity, a competitive risk, a policy lesson.

### 🤖 AI Monetization Opportunities for India

The reader is a software engineer who wants **buildable AI product ideas**, not buzzwords.

Scan the Tech, Business, Economy, and China stories for a trend or technology where (a) AI is the enabler, and (b) a product or service for the Indian market is plausible. For each opportunity (target 1-4; quality over quantity):

- **The signal** — the story or trend it comes from.
- **The concept** — a specific AI product or service. Concrete enough to picture. Not "use AI for logistics" but "an AI route-and-load optimizer sold to mid-size Indian truck fleets".
- **Indian market & monetization** — who pays, and how: B2B SaaS subscription, per-API-call pricing, consumer freemium, marketplace take-rate, etc. Name a target segment.
- **Feasibility** — favor what a small technical team can ship; the reader builds software, not factories. Flag clearly when an idea is capital-heavy, hardware-dependent, or sits in a regulated space (fintech, health) so the reader can judge.

Be honest when an idea is thin. One strong, well-reasoned opportunity beats four hand-wavy ones.

## Closing spoken summary

After saving the file, don't just report the path. Give the user a quick 3-5 line readout: the single biggest story, and the standout item from each of the two analysis sections. That's their "morning briefing" if they only have ten seconds.
