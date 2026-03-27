# Roadmap — travel-search

## v1.0.0 ✅ (Released 2026-03-26)
- [x] Kiwi.com MCP — flights with creative routing
- [x] Skiplagged MCP — flights + hotels + car rentals
- [x] Trivago MCP — hotel price comparison
- [x] Ferryhopper MCP — ferries across 33 countries
- [x] Google Flights via fli (optional, requires local install)
- [x] Helper script (mcp-call.sh)
- [x] Published on ClawHub + GitHub

## v1.1.0 ✅ — Trip Planner
- [x] Full itinerary generation: flight + hotel + day-by-day plan
- [x] Budget breakdown: flight + hotel + estimated food + local transport
- [x] "Plan me 5 days in Rome for €800" → complete trip with real prices
- [x] Multi-provider combination (cheapest flight + best-value hotel)
- [x] Daily cost estimates by region (Europe, Asia, Latin America, etc.)
- [x] Day-by-day itinerary with morning/afternoon/evening activities
- [x] Add `references/trip-planner.md`

## v1.2.0 ✅ — Smart Price & Value Engine
- [x] Value scoring system: price × quality × convenience → single best recommendation
- [x] Cross-provider comparison engine (Kiwi + Skiplagged parallel search, deduplication, scoring)
- [x] Price calendar via sk_flex_departure_calendar and sk_flex_return_calendar
- [x] "Anywhere" search for flexible destinations (sk_destinations_anywhere)
- [x] Hotel scoring: rating × price × location × amenities
- [x] Deal detection with benchmarks ("🔥 40% below average!")
- [x] Complete decision tree: what to search when
- [x] Trade-off explanations for every alternative
- [x] Hidden cost flagging (baggage, breakfast, insurance)
- [x] Add `references/price-tools.md`

## v1.3.0 ✅ — Airbnb Integration
- [x] Integrate Airbnb MCP docs (`@openbnb/mcp-server-airbnb` via local `npx`)
- [x] Short-stay vs hotel automatic comparison workflow
- [x] Defaults for when Airbnb wins vs hotels by trip type
- [x] Airbnb value scoring (space, amenities, privacy, policies)
- [x] "What's cheaper, Airbnb or hotel in Barcelona for 5 nights?"
- [x] Add `references/airbnb.md`

## v1.4.0 ✅ — Multi-city Optimizer
- [x] Route optimization: "Visit Rome, Paris, Amsterdam in 10 days"
- [x] Price matrix builder for inter-city flights
- [x] Geographic flow optimization (minimize backtracking)
- [x] Smart day allocation by city size
- [x] Open-jaw flight detection (fly into A, out of C)
- [x] Hub city awareness for cheaper first/last legs
- [x] Train/bus suggestion for short hops (<500km)
- [x] Cluster-based optimization for 5+ cities
- [x] Add `references/multi-city.md`

## v1.5.0 ✅ — Travel Intel
- [x] Weather forecasts via wttr.in + best travel season patterns by region
- [x] Visa quick reference with passport-power tiers
- [x] Currency, cards, ATMs, and tipping culture by region
- [x] Local transport guides: airport transfers + city transit for major cities
- [x] Safety notes (scams, neighborhoods, health) when relevant
- [x] Power plugs and connectivity (SIM/eSIM, WiFi)
- [x] Concise presentation format (8-12 lines, first-time visitor essentials)
- [x] Add `references/travel-intel.md`

## v2.0 Roadmap — Next Level

### v2.1 — Train & Bus Search
- [ ] Train APIs (Trainline, Renfe, Trenitalia, DB, SNCF)
- [ ] Bus APIs (Flixbus, ALSA, Eurolines, Greyhound)
- [ ] Auto-suggest train/bus when cheaper or more convenient than flying
- [ ] Integrated into multi-city optimizer: mixed transport routes (fly A→B, train B→C)

### v2.2 — Price Tracking & Alerts
- [ ] "Track this flight and alert me if price drops"
- [ ] Periodic price monitoring via cron/heartbeat
- [ ] Historical price context ("this route is usually $X, right now it's $Y")
- [ ] Push notification to user when target price hit

### v2.3 — Packing & Preparation
- [ ] Smart packing list based on destination + weather + trip duration + vibe
- [ ] Checklist: documents, insurance, vaccinations, apps to download
- [ ] Destination-specific prep ("download offline maps", "get Japan Rail Pass", etc.)

### v2.4 — Group Trip Coordinator
- [ ] Split costs calculator for group trips
- [ ] Shared itinerary format (exportable, collaborative)
- [ ] Voting system: "everyone pick your top 3 cities" → optimize from group preferences
- [ ] Budget fairness: different budget tiers within same group

### v2.5 — Booking Memory & Loyalty
- [ ] Remember user's past searches and preferences
- [ ] "I always prefer window seats and morning flights"
- [ ] Track loyalty programs: "I have miles on United, use them when possible"
- [ ] Saved destinations wishlist: "I want to go here someday"

### v2.6 — Real-Time Trip Companion
- [ ] Day-of assistance: "what's open near me right now?"
- [ ] Weather alerts during trip: "rain expected at 3 PM, move outdoor plans to morning"
- [ ] Restaurant recommendations based on current location + vibe
- [ ] "My flight got cancelled, what are my options?"

### v2.7 — Experiences & Activities
- [ ] Integration with activity/tour booking APIs (GetYourGuide, Viator)
- [ ] "Find me a cooking class in Rome" → real prices + booking
- [ ] Event detection: "there's a festival happening during your dates!"
- [ ] Free walking tour recommendations per city

### v2.8 — Travel Insurance Comparison
- [ ] Compare travel insurance options
- [ ] "Do I need insurance for this trip?"
- [ ] Coverage recommendations based on destination + activities

## Future Ideas (when APIs/tech allows)
- [ ] Property/rental search (Idealista, Fotocasa — when APIs become available)
- [ ] Long-term stay optimization (1-6 months, digital nomad focused)
- [ ] Carbon footprint calculation and eco-routing
- [ ] AR/photo preview of destinations
- [ ] Trip journal/diary generator from photos
- [ ] Offline mode: downloadable trip info packet
