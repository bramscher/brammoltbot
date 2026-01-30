# Konmashi Campaign Specs — Executive Summary

## Three Campaigns to Build

| # | Campaign | Target Audience | Primary Goal |
|---|----------|-----------------|--------------|
| 1 | HDPM Vacancy Marketing | Renters in Central Oregon | Fill vacancies faster via automated social |
| 2 | Konmashi for PM Companies | Property management companies (Appfolio users) | Acquire Konmashi customers |
| 3 | Wellifi (Remy + MED) | Health-conscious consumers | Drive subscriptions |

---

## Campaign 1: HDPM Vacancy Marketing

**What Konmashi needs to do:**
- Connect to Appfolio API and pull vacancy data (property details, photos, rent, availability)
- Automatically generate social content when a new vacancy appears
- Post to Instagram, TikTok, YouTube
- Track performance and update when properties lease

**Content types:**
- AI avatar property tour videos (15-30 sec)
- Photo carousels with property details
- "Just Listed" announcements
- Neighborhood spotlight videos (monthly)

**Data flow:**
```
Appfolio vacancy → Konmashi → Generated content → Social platforms
```

**See:** `01-hdpm-vacancy-marketing.md` for full spec including data fields, templates, and posting cadence.

---

## Campaign 2: Konmashi for PM Companies

**What Konmashi needs to do:**
- Generate B2B marketing content targeting PM company owners
- Showcase Konmashi's Appfolio integration value
- Use HDPM as the case study / proof point
- Drive demo requests and sign-ups

**Content types:**
- Problem/solution AI avatar videos ("No time for marketing? We solve that.")
- Feature demo carousels ("How it works in 5 slides")
- Case study content (once HDPM has results)
- PM industry thought leadership

**Key message:**
"Turn your Appfolio vacancies into social media content — automatically."

**See:** `02-konmashi-for-pm-companies.md` for full spec including scripts, platform strategy, and B2B targeting.

---

## Campaign 3: Wellifi (Remy + MED)

**Two products:**
1. **Remy** — AI meal planning (personalized meals, grocery lists, adapts to preferences)
2. **MED** — "Blinkist for health podcasts" (10-min audio summaries of 2-hour episodes)

**What Konmashi needs to do:**
- Generate consumer-focused content for health/wellness audience
- Create educational + entertaining content ("edutainment")
- Drive free trials and subscriptions

**Content types:**
- "What I eat in a day" videos (Remy)
- Meal plan reveal carousels (Remy)
- Podcast summary teasers — "I listened to 2hrs of Huberman so you don't have to" (MED)
- Health tip quick hits from podcast summaries (MED)

**Key messages:**
- Remy: "Eat better without thinking about it."
- MED: "Get smarter about health in 10 minutes a day."

**See:** `03-wellifi-remy-med.md` for full spec including content templates, posting cadence, and hashtag strategy.

---

## Output Requirements (All Campaigns)

### Platforms
| Platform | Content Format |
|----------|---------------|
| Instagram | Reels (15-60s), Carousels (5-7 slides), Stories |
| TikTok | Short videos (15-60s) |
| YouTube | Shorts (15-60s), longer videos for tutorials/case studies |
| Facebook | Carousels, videos (same as Instagram) |
| LinkedIn | B2B content for Campaign 2 only |

### Content Formats
1. **AI Avatar Videos** — Heygen-style talking head presenting info
2. **Carousels** — Multi-slide image posts with text overlays
3. **Quick-hit videos** — Fast-paced, hook-heavy content
4. **Static posts** — Image + caption for announcements

### Technical Integrations
- **Heygen** (or similar) — AI avatar video generation
- **Appfolio API** — Property vacancy data for Campaign 1
- **Meta API** — Instagram/Facebook posting
- **TikTok API** — TikTok posting
- **YouTube API** — YouTube Shorts / video uploads
- **LinkedIn API** — B2B content posting (Campaign 2)

---

## Dev Handoff Checklist

For each campaign, developers should confirm:

- [ ] Data source integration (Appfolio for Campaign 1, manual/Wellifi for Campaign 3)
- [ ] Content template system (variable insertion, asset management)
- [ ] AI avatar generation pipeline (Heygen or equivalent)
- [ ] Carousel/image generation (templated graphics with dynamic text)
- [ ] Multi-platform posting automation
- [ ] Scheduling / cadence rules
- [ ] Analytics / performance tracking
- [ ] Approval workflow (if needed before posting)

---

## Priority Order

1. **Campaign 1 (HDPM)** — Proving ground. Build here first. Demonstrates Konmashi value with real data.
2. **Campaign 2 (Konmashi B2B)** — Use Campaign 1 results as proof points. Meta play.
3. **Campaign 3 (Wellifi)** — Consumer marketing. Can run in parallel once content system is built.

---

## File Index

| File | Description |
|------|-------------|
| `00-executive-summary.md` | This file — overview for leadership |
| `01-hdpm-vacancy-marketing.md` | Full spec for HDPM campaign |
| `02-konmashi-for-pm-companies.md` | Full spec for Konmashi B2B campaign |
| `03-wellifi-remy-med.md` | Full spec for Wellifi consumer campaign |
