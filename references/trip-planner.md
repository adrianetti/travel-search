# Trip Planner — Full Itinerary Generator

Generate complete trip itineraries with real prices by combining multiple providers.

## When to Use

Trigger phrases:
- "Plan me a trip to..."
- "I want to visit X for Y days"
- "Make me an itinerary for..."
- "Plan a vacation to..."
- "Trip to X with budget of €Y"

## Workflow

### Step 1: Gather Requirements

Extract from user request (ask if missing):
- **Destination(s)** — city/cities
- **Origin** — departure city
- **Dates** — specific or flexible ("sometime in April")
- **Duration** — number of days
- **Budget** — total or "cheap as possible"
- **Travelers** — number of adults/children
- **Preferences** — hotel stars, cabin class, interests (culture, food, nightlife, nature)

### Step 2: Search Flights

Use Kiwi (read `references/flights.md`):
```bash
# If dates are flexible, search with departureDateFlexRange: 3
# Sort by price first
# Get top 3-5 options
```

If budget is tight, also check Skiplagged for hidden city fares (read `references/skiplagged.md`).

Pick the **best value** flight (not just cheapest — consider duration and layover quality).

### Step 3: Search Accommodation

Calculate check-in = arrival date, check-out = departure date.

Use Skiplagged for hotels (read `references/skiplagged.md`):
```bash
# sk_hotels_search with city, checkin, checkout, guests
```

Cross-check with Trivago (read `references/hotels.md`) for price comparison.

Present 2-3 hotel options across budget tiers:
- 💰 Budget — cheapest decent option
- ⭐ Mid-range — best value (price vs rating)
- 💎 Premium — best rated

### Step 4: Build Budget Breakdown

Estimate daily costs based on destination:

| Category | Budget Tier | Mid Tier | Premium Tier |
|----------|-------------|----------|--------------|
| Flight | actual price | actual price | actual price |
| Hotel | actual price | actual price | actual price |
| Food | estimate/day | estimate/day | estimate/day |
| Transport | estimate/day | estimate/day | estimate/day |
| Activities | estimate/day | estimate/day | estimate/day |

**Daily cost estimates by region** (per person):

Western Europe (Paris, London, Amsterdam):
- Budget: €40-60/day (food + transport + activities)
- Mid: €80-120/day
- Premium: €150+/day

Southern Europe (Rome, Barcelona, Lisbon):
- Budget: €30-50/day
- Mid: €60-100/day
- Premium: €120+/day

Southeast Asia (Bangkok, Bali, Hanoi):
- Budget: €15-25/day
- Mid: €30-50/day
- Premium: €80+/day

Japan:
- Budget: €40-60/day
- Mid: €80-120/day
- Premium: €150+/day

Latin America (Mexico City, Buenos Aires, Medellín):
- Budget: €20-35/day
- Mid: €40-70/day
- Premium: €100+/day

### Step 5: Generate Day-by-Day Itinerary

Structure each day:

```
📅 Day 1 — [Date] — Arrival
- ✈️ Flight: [origin] → [destination] ([time])
- 🏨 Check-in: [hotel name]
- 🌆 Evening: [neighborhood to explore] — dinner at [area recommendation]

📅 Day 2 — [Date] — [Theme: e.g., "Historic Center"]
- 🌅 Morning: [activity/attraction]
- 🍽️ Lunch: [area/cuisine suggestion]
- 🌇 Afternoon: [activity/attraction]
- 🌙 Evening: [dinner area / nightlife suggestion]

...

📅 Day N — [Date] — Departure
- 🏨 Check-out
- [Morning activity if time allows]
- ✈️ Flight: [destination] → [origin] ([time])
```

### Step 6: Present the Itinerary

Format for Discord/chat (no markdown tables):

```
✈️ [DESTINATION] — [DURATION] days | [DATES]

💰 Budget Summary
- Flight: €XXX (round trip) — [booking link]
- Hotel: €XXX ([N] nights) — [booking link]
- Daily expenses: ~€XX/day × [N] days = €XXX
- **Total estimated: €XXX**

🏨 Hotel: [Name] — [rating] — [price/night]

📅 Day-by-day:
[... itinerary ...]

🔗 Book now:
- Flight: [deep link]
- Hotel: [deep link]
```

## Tips

- Always include booking links for flight and hotel
- If user has a budget constraint, work backwards: budget - flight = remaining for hotel + daily
- For multi-day trips, suggest a mix of activities (don't overload every day)
- Include 1 "free day" for trips > 5 days (rest / spontaneous exploration)
- Mention best neighborhoods to stay in for the destination
- Consider arrival/departure times when planning Day 1 and last day
- If flight arrives late, Day 1 is just check-in + dinner area
- If flight departs early, last day is just departure
