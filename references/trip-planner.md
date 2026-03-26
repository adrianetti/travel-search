# Trip Planner — Universal Itinerary Generator

Generate complete, personalized trip itineraries with real prices and booking links. Adapts to any traveler, any destination, any style.

## Step 1: Profile the Trip

Extract these signals from the user's request. **Ask only what's missing and critical** (destination + dates minimum). Infer the rest from context.

### Required
- **Destination(s)** — city, country, or region
- **Origin** — where they're departing from
- **Dates** — specific or flexible ("sometime in June", "cheapest week")
- **Duration** — number of days/nights

### Infer or Ask If Unclear

**Budget Tier** — detect from language cues:
- "cheap / budget / backpacking / save money" → Budget
- "nice / comfortable / good value" → Mid-range
- "luxury / splurge / treat myself / premium / 5-star" → Premium
- No mention → default to Mid-range

**Travel Party:**
- Solo traveler
- Couple / romantic getaway / honeymoon
- Friends group / bachelor/bachelorette
- Family with young kids (0-5)
- Family with older kids (6-12)
- Family with teenagers (13-17)
- Multi-generational (grandparents + parents + kids)
- Business + leisure (bleisure)

**Trip Vibe** — the core personality of the trip. People rarely say one word; detect from overall intent:

Cultural & Historic:
- Museums, galleries, architecture, ruins, UNESCO sites
- "I want to see the history" / "cultural trip" / "love museums"

Food & Drink:
- Local cuisine, street food, fine dining, food tours, cooking classes, wine/beer
- "foodie trip" / "I want to eat everything" / "gastronomy" / "wine tour"

Adventure & Outdoors:
- Hiking, diving, surfing, skiing, climbing, kayaking, safaris, national parks
- "adventure" / "outdoor" / "active trip" / "adrenaline"

Beach & Relaxation:
- Beach, spa, resort, pool, slow mornings, no agenda
- "relax" / "chill" / "do nothing" / "decompress" / "zen"

Party & Nightlife:
- Clubs, bars, rooftops, live music, festivals, pub crawls
- "party" / "nightlife" / "clubs" / "we want to go out"

Romance:
- Intimate dinners, scenic spots, couples activities, privacy
- "anniversary" / "honeymoon" / "romantic" / "with my partner"

Shopping:
- Markets, boutiques, outlets, luxury brands, souvenirs, local crafts
- "shopping trip" / "I want to shop" / "outlets"

Wellness & Health:
- Yoga retreats, spas, meditation, thermal baths, detox, health resorts
- "wellness" / "retreat" / "yoga" / "spa trip" / "self-care"

Photography & Scenic:
- Viewpoints, golden hour spots, photogenic locations, landscapes
- "I want amazing photos" / "scenic" / "Instagram spots" / "photography"

Nature & Wildlife:
- Bird watching, whale watching, national parks, botanical gardens, eco-tourism
- "nature" / "wildlife" / "eco" / "animals" / "birdwatching"

Spiritual & Pilgrimage:
- Temples, churches, meditation centers, pilgrimage routes (Camino de Santiago, etc.)
- "spiritual" / "pilgrimage" / "temples" / "finding myself"

Sports & Events:
- Football matches, F1, tennis, Olympics, marathons, local sports events
- "I want to see a match" / "sports" / "football" / "F1"

Music & Festivals:
- Concerts, festivals (Tomorrowland, Coachella, Primavera), opera, jazz clubs
- "festival" / "concert" / "music" / "live shows"

Family Fun:
- Theme parks, zoos, aquariums, kid-friendly activities, educational
- "with the kids" / "family friendly" / "what can kids do"

Digital Nomad / Work:
- Coworking spaces, good WiFi, cafés to work, long-stay, time zone friendly
- "working remotely" / "digital nomad" / "need wifi" / "workcation"

Road Trip:
- Scenic drives, car rental, multiple stops, freedom, countryside
- "road trip" / "drive around" / "rent a car and explore"

Luxury & Exclusive:
- Michelin stars, private tours, first class, penthouses, VIP access
- "luxury" / "splurge" / "money is not an issue" / "VIP"

Backpacking & Budget:
- Hostels, street food, public transport, free activities, off-beaten-path
- "backpacking" / "on a budget" / "cheap" / "hostel life"

Off the Beaten Path:
- Hidden gems, non-touristy, local neighborhoods, authentic experiences
- "not touristy" / "hidden gems" / "local experience" / "authentic"

Voluntourism & Impact:
- Volunteering, community projects, eco-volunteering, teaching
- "volunteer" / "give back" / "community project"

Learning & Courses:
- Language immersion, cooking classes, art workshops, university tours
- "learn something" / "take a class" / "language immersion"

Medical & Health Tourism:
- Dental work, surgery, treatments, recovery + tourism combo
- "medical trip" / "dental" / "getting a procedure"

LGBTQ+ Friendly:
- Welcoming destinations, pride events, queer-friendly neighborhoods
- "LGBTQ friendly" / "pride" / "gay-friendly"

Accessibility:
- Wheelchair accessible, limited mobility, sensory-friendly, medical needs
- "wheelchair" / "accessible" / "mobility issues" / "disabled"

Pet-Friendly:
- Dog-friendly hotels, parks, restaurants, transport policies
- "traveling with my dog" / "pet friendly"

Eco & Sustainable:
- Low carbon, train over plane, eco-lodges, carbon offset, sustainable tourism
- "eco-friendly" / "sustainable" / "green travel" / "low carbon"

**When no vibe is specified:** Default to a balanced mix — 40% cultural/historic, 30% food, 20% local neighborhoods, 10% relaxation. This works for 80%+ of travelers.

**When multiple vibes are mentioned:** Blend them proportionally in the itinerary.

### Additional Preferences (detect if mentioned)

**Pace:**
- Packed (something every 2-3 hours)
- Moderate (2-3 activities per day with free time)
- Relaxed (1-2 things per day, lots of downtime)
- Default: Moderate

**Dietary:**
- Vegetarian, vegan, halal, kosher, gluten-free, allergies
- Affects restaurant recommendations

**Accommodation style:**
- Hotel, hostel, Airbnb, resort, boutique hotel, camping, glamping, villa, ryokan
- Budget tier usually implies this, but user may override

**Transport preference:**
- Public transit, walking-heavy, taxi/Uber, rental car, bike
- Affects daily logistics

**Time of day preference:**
- Early bird vs late riser
- Affects scheduling (some travelers hate 8 AM museum visits)

## Step 2: Search Flights

Read `references/flights.md` (Kiwi) or `references/skiplagged.md`.

Strategy by budget:
- **Budget:** Sort by price, accept longer layovers. Try `departureDateFlexRange: 3` for cheaper dates.
- **Mid-range:** Sort by quality (price × duration balance). Prefer ≤1 stop.
- **Premium:** Sort by duration, prefer direct flights or business class (`cabinClass: "C"`).

Always show:
- 💸 Cheapest option
- ⚡ Fastest option
- 🎯 Best value (recommended)

Include deep link for each.

## Step 3: Search Accommodation

Read `references/skiplagged.md` (hotels) and/or `references/hotels.md` (Trivago).

Match to budget + vibe:
- **Budget:** Filter for cheapest. Mention hostels if backpacking vibe.
- **Mid-range:** Best price-to-rating ratio. 3-4★, rating ≥ 8.0.
- **Premium:** Highest rated. 4-5★, mention unique features (pool, rooftop, spa).

Location matters:
- Recommend neighborhoods based on vibe (party → near nightlife, cultural → near old town, etc.)
- Always mention how far from city center / main attractions.

Present 2-3 options across tiers even if user specified a budget (gives them choice).

## Step 4: Budget Breakdown

Calculate real costs + estimates:

```
Flight:        $XXX (actual from search)
Hotel:         $XXX (actual from search, N nights)
Daily costs:   $XX/day × N days = $XXX
  ├─ Food:     based on destination + budget tier
  ├─ Transport: based on destination + transport preference  
  └─ Activities: based on vibe + destination
─────────────────────────────────
TOTAL:         $X,XXX
```

### Daily Cost Benchmarks (per person, USD)

**Western Europe** (Paris, London, Amsterdam, Zurich):
- Budget: $40-60 | Mid: $80-130 | Premium: $160+

**Southern Europe** (Rome, Barcelona, Lisbon, Athens, Istanbul):
- Budget: $30-50 | Mid: $60-100 | Premium: $130+

**Eastern Europe** (Prague, Budapest, Krakow, Belgrade):
- Budget: $20-35 | Mid: $40-70 | Premium: $100+

**Scandinavia** (Stockholm, Copenhagen, Oslo, Helsinki):
- Budget: $50-70 | Mid: $90-140 | Premium: $180+

**UK & Ireland** (London, Edinburgh, Dublin):
- Budget: $40-60 | Mid: $80-130 | Premium: $160+

**USA & Canada** (NYC, LA, Toronto, Vancouver):
- Budget: $50-70 | Mid: $90-150 | Premium: $200+

**Japan:**
- Budget: $40-60 | Mid: $80-130 | Premium: $170+

**South Korea:**
- Budget: $30-50 | Mid: $60-100 | Premium: $130+

**Southeast Asia** (Bangkok, Bali, Hanoi, Kuala Lumpur):
- Budget: $15-25 | Mid: $35-60 | Premium: $90+

**South Asia** (India, Sri Lanka, Nepal):
- Budget: $10-20 | Mid: $25-50 | Premium: $80+

**China:**
- Budget: $20-35 | Mid: $50-80 | Premium: $120+

**Middle East** (Dubai, Doha, Amman):
- Budget: $40-60 | Mid: $80-140 | Premium: $200+

**Latin America** (Mexico City, Buenos Aires, Medellín, Lima):
- Budget: $15-30 | Mid: $35-65 | Premium: $100+

**Caribbean** (Dominican Republic, Cuba, Puerto Rico):
- Budget: $30-50 | Mid: $60-100 | Premium: $150+

**Africa** (Morocco, Kenya, South Africa, Egypt):
- Budget: $15-30 | Mid: $40-80 | Premium: $120+

**Australia & New Zealand:**
- Budget: $50-70 | Mid: $90-140 | Premium: $180+

**Pacific Islands** (Fiji, Tahiti, Maldives):
- Budget: $40-60 | Mid: $80-150 | Premium: $250+

## Step 5: Build Day-by-Day Itinerary

### Structure

```
📅 Day X — [Date] ([Day of week]) — [Theme/Neighborhood]
🌅 Morning: [activity]
🍽️ Lunch: [area/cuisine/specific spot if known]
🌇 Afternoon: [activity]
🍽️ Dinner: [area/cuisine suggestion]
🌙 Evening: [optional: nightlife, show, rooftop, walk]
💡 Tip: [practical tip for this day]
```

### Rules

1. **Day 1 = Arrival.** Account for flight arrival time. If arriving late, Day 1 is just check-in + nearby dinner/walk. If arriving early, add an afternoon activity.

2. **Last Day = Departure.** If flying late, add a morning activity. If flying early, just check-out.

3. **Rest Day.** For trips > 5 days, include one lighter day (sleep in, no fixed plans, spontaneous exploration). Usually day 4 or 5.

4. **Geography clustering.** Group activities by neighborhood/area per day to minimize transit time.

5. **Timing awareness:**
   - Museums: go early (less crowded) or late afternoon
   - Markets: mornings are best
   - Parks: afternoon golden hour
   - Nightlife: starts late in Southern Europe / Latin America (10 PM+)
   - Religious sites: check prayer times and dress codes

6. **Pacing by preference:**
   - Packed: 4-5 activities per day
   - Moderate: 2-3 activities + free time
   - Relaxed: 1-2 activities + wandering

7. **Vibe integration:** Weight activities toward the detected vibe. Foodie trip? Every meal is a highlight. Adventure? Include a day trip. Cultural? Hit the top 3 museums.

8. **Local knowledge:** Mention:
   - Best time to visit each attraction
   - Free entry days (many European museums have them)
   - Neighborhoods to walk through
   - Local customs or etiquette
   - Tipping culture
   - Safety notes if relevant

9. **Day trip options.** For 5+ day trips, suggest 1 nearby excursion:
   - Paris → Versailles
   - Madrid → Toledo or Segovia
   - Rome → Pompeii or Tivoli
   - Tokyo → Kamakura or Hakone
   - Barcelona → Montserrat
   - London → Stonehenge or Bath

## Step 6: Present the Itinerary

Format for Discord/chat (no markdown tables, use bullet lists):

```
✈️ [DESTINATION] — [N] days | [DATES]

[One-line vibe summary: "Cultural + foodie trip on a mid-range budget"]

💰 Budget Summary
- ✈️ Flight: $XXX round trip — [link]
- 🏨 Hotel: $XXX (N nights, [hotel name]) — [link]
- 🍽️🚇🎟️ Daily: ~$XX/day × N days = $XXX
- 💵 **Total: ~$X,XXX**

🏨 [Hotel name] — [stars]★ [rating]/10 — $XX/night
📍 [Neighborhood] — [why it's good for their vibe]

📅 Day-by-day itinerary...

🔗 Book Now:
- Flight: [deep link]
- Hotel: [deep link]

💡 Pro tips:
- [2-3 destination-specific tips]
```

### Adaptation Examples

"Plan me a cheap backpacking trip to Southeast Asia for 3 weeks":
→ Budget tier, hostels, street food, local transport, packed schedule, adventure + cultural vibe

"Honeymoon in Santorini, money is not an issue":
→ Premium tier, boutique hotel with caldera view, romantic dinners, sunset spots, relaxed pace

"Family trip to Orlando with 2 kids under 10":
→ Mid-range, family hotel with pool, theme parks, kid-friendly restaurants, moderate pace

"I want to eat my way through Tokyo for 5 days":
→ Gastro vibe, mid-range, hotel near Shinjuku/Shibuya, every meal is the highlight, include Tsukiji, ramen alleys, izakayas, cooking class

"Work trip to London, want to see some stuff on the side":
→ Bleisure, efficient schedule, hotel with good WiFi, evening/weekend activities only

"Road trip through Patagonia":
→ Adventure vibe, car rental, multiple stops, camping/lodges, nature-focused, flexible schedule
