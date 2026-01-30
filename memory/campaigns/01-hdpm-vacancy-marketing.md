# Campaign 1: High Desert Property Management — Vacancy Marketing

## Overview
Automatically generate social media content for vacant rental properties managed by High Desert PM. Content pulls live data from Appfolio and creates engaging posts to fill vacancies faster.

## Data Source: Appfolio Integration
Konmashi needs to pull the following data from Appfolio API for each vacant unit:

### Required Data Fields
```
Property:
- property_id
- property_name
- address (street, city, state, zip)
- property_type (apartment, house, townhome, etc.)
- neighborhood/area name

Unit:
- unit_id
- unit_number (if applicable)
- bedrooms
- bathrooms
- square_footage
- rent_price (monthly)
- available_date
- pet_policy (dogs/cats/none/negotiable)
- parking (garage, covered, street, etc.)
- laundry (in-unit, on-site, none)

Amenities:
- List of amenities (dishwasher, A/C, fireplace, etc.)
- Community amenities (pool, gym, etc.)

Media:
- photo_urls[] (unit photos)
- video_url (if virtual tour exists)
- floor_plan_url (if available)
```

### Data Refresh Frequency
- Pull vacancy data daily (or on webhook when status changes)
- Archive content when unit is leased
- Re-activate content if unit becomes available again

---

## Content Types

### 1. Property Showcase Video (AI Avatar)
**Platform:** Instagram Reels, TikTok, YouTube Shorts
**Duration:** 15-30 seconds
**Format:** AI avatar (Heygen) presenting the property

**Script Template:**
```
[HOOK - 2 sec]
"Looking for a {bedrooms}-bed in {city}? 👀"

[BODY - 10-20 sec]
"This {property_type} in {neighborhood} has {highlight_1}, {highlight_2}, and {highlight_3}. 
{square_footage} square feet for just ${rent_price} a month.
{pet_policy_statement}
Available {available_date}."

[CTA - 3 sec]
"Link in bio to schedule a tour — this one won't last! 🏠"
```

**Dynamic Variables:**
- {bedrooms}, {city}, {property_type}, {neighborhood}
- {highlight_1/2/3} = top 3 amenities (auto-selected or prioritized)
- {square_footage}, {rent_price}, {available_date}
- {pet_policy_statement} = "Pet friendly!" / "Cats welcome!" / etc.

**Visual Assets:**
- B-roll: cycle through property photos
- Text overlays: rent price, beds/baths, key amenities
- End card: HDPM logo + "Link in Bio"

---

### 2. Property Carousel (Instagram/Facebook)
**Platform:** Instagram, Facebook
**Format:** 5-7 image carousel with text overlays

**Slide Structure:**
```
Slide 1 (Hook): Hero photo + "{bedrooms}BR in {city} — ${rent_price}/mo"
Slide 2: Interior shot + "✨ {highlight_1}"
Slide 3: Kitchen/bathroom shot + "✨ {highlight_2}"  
Slide 4: Bedroom/living shot + "✨ {highlight_3}"
Slide 5: Exterior/neighborhood + "📍 {neighborhood} location"
Slide 6: Details card (beds, baths, sqft, available date, pet policy)
Slide 7: CTA — "DM us or tap link in bio to schedule a tour"
```

**Caption Template:**
```
🏠 {bedrooms}BR {property_type} in {neighborhood}, {city}

✅ {amenity_1}
✅ {amenity_2}
✅ {amenity_3}
✅ {pet_policy}

💰 ${rent_price}/month
📅 Available {available_date}

👉 Link in bio to apply or schedule a tour!

#RentCentralOregon #{city}Rentals #ApartmentHunting #{city}Living #PetFriendlyRentals
```

---

### 3. "Just Listed" Announcement
**Platform:** All platforms
**Format:** Quick 7-second video or static image
**Purpose:** Urgency/FOMO for new listings

**Script:**
```
"🚨 JUST LISTED: {bedrooms}BR in {city} for ${rent_price}/mo. Link in bio before it's gone!"
```

---

### 4. Neighborhood Spotlight (Monthly)
**Platform:** YouTube, Instagram Reels
**Format:** 60-90 second AI avatar video
**Purpose:** SEO + brand building for each area HDPM serves

**Content:**
- Why people love living in {neighborhood}
- Local highlights (restaurants, parks, activities)
- Current availability in that area
- CTA to browse listings

---

## Posting Cadence

| Trigger | Content Type | Platforms |
|---------|--------------|-----------|
| New vacancy | "Just Listed" announcement | All |
| New vacancy | Full showcase video (within 24h) | Reels, TikTok, Shorts |
| New vacancy | Property carousel (within 48h) | Instagram, Facebook |
| Weekly | "Available Now" roundup (all vacancies) | Stories, TikTok |
| Monthly | Neighborhood spotlight | YouTube, Reels |
| Price drop | "Price Reduced" announcement | All |

---

## Hashtag Strategy

**Location-based:**
- #BendOregon #BendRentals #CentralOregonLiving #RedmondOregon #SistersOregon
- #{City}Apartments #{City}Homes

**Interest-based:**
- #ApartmentHunting #RentalSearch #MovingTo{City} #PetFriendlyRentals
- #FirstApartment #RemoteWorkFriendly

**Branded:**
- #HighDesertPM #HighDesertPropertyManagement

---

## Success Metrics (for Konmashi dashboard)

- Views per property video
- Engagement rate (likes, comments, shares)
- Link clicks / bio taps
- Inquiries attributed to social (track with UTM)
- Days on market (before vs after campaign)
- Cost per lead (if running paid)

---

## Technical Requirements for Devs

### Appfolio API Integration
1. Authenticate with Appfolio API (OAuth or API key)
2. Pull vacancy data on schedule or webhook
3. Map Appfolio fields to Konmashi content variables
4. Handle missing data gracefully (default values or skip field)

### Content Generation Pipeline
1. Receive new/updated vacancy data
2. Select content templates based on property type and available assets
3. Generate AI avatar video (Heygen API integration)
4. Generate carousel images (templated graphics with dynamic text)
5. Queue content for posting per cadence rules
6. Post to connected social accounts via Meta API, TikTok API, YouTube API

### Asset Management
- Store property photos locally or reference Appfolio CDN
- Generate thumbnails for video posts
- Create consistent branded templates (HDPM colors, logo)

---

## Open Questions for HDPM Team
- [ ] What Appfolio API access level do we have?
- [ ] Are there existing property photos, or do we need to request uploads?
- [ ] Preferred AI avatar (existing HDPM spokesperson or generic)?
- [ ] Any properties/areas to exclude from social posting?
- [ ] Approval workflow needed before posting, or fully automated?
