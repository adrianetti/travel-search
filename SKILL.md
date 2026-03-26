---
name: travel-search
description: "Search flights, hotels, car rentals, and ferries across multiple providers using free APIs. Plan complete trip itineraries with real prices and booking links. Use when: user asks about flights, travel, hotels, accommodation, car rentals, ferry routes, trip planning, vacation planning, itinerary generation, finding cheap flights, comparing travel options, planning multi-city routes, or budget travel. Covers Kiwi.com (flights), Skiplagged (flights + hotels + cars), Trivago (hotels), Ferryhopper (ferries), and Google Flights via fli. All primary providers are free with no API key required."
metadata: { "openclaw": { "emoji": "✈️", "requires": { "bins": ["curl"] } } }
---

# Travel Search

Search flights, hotels, car rentals, and ferries across multiple free providers via MCP protocol.

## Quick Reference

| Need | Provider | Reference |
|------|----------|-----------|
| Flights (creative routing) | Kiwi.com | [flights.md](references/flights.md) |
| Flights + Hotels + Cars | Skiplagged | [skiplagged.md](references/skiplagged.md) |
| Hotels (price comparison) | Trivago | [hotels.md](references/hotels.md) |
| Ferries | Ferryhopper | [ferries.md](references/ferries.md) |
| Flights (Google Flights) | fli | [google-flights.md](references/google-flights.md) |
| Full trip itinerary | Multi-provider | [trip-planner.md](references/trip-planner.md) |

## How It Works

All providers use the MCP protocol (JSON-RPC 2.0 over HTTP). Call them with `curl`:

```bash
# 1. Initialize session
curl -s -X POST "$MCP_URL" \
  -H "Content-Type: application/json" \
  -H "Accept: application/json, text/event-stream" \
  -d '{"jsonrpc":"2.0","id":1,"method":"initialize","params":{"protocolVersion":"2025-06-18","capabilities":{},"clientInfo":{"name":"openclaw","version":"1.0"}}}'

# 2. Extract Mcp-Session-Id from response headers (if returned)

# 3. Call a tool
curl -s -X POST "$MCP_URL" \
  -H "Content-Type: application/json" \
  -H "Accept: application/json, text/event-stream" \
  -H "Mcp-Session-Id: $SESSION_ID" \
  -d '{"jsonrpc":"2.0","id":2,"method":"tools/call","params":{"name":"TOOL_NAME","arguments":{...}}}'
```

Response format: SSE with `event: message` + `data: {JSON}`. Parse the `data` line.

## Decision Guide

### User wants flights
1. **Start with Kiwi** — best for creative routing (combining airlines) and European routes
2. **Cross-check with Skiplagged** — hidden city fares can be cheaper
3. **Use fli (Google Flights)** if installed — widest coverage, flexible date search
4. Present the best 3-5 options with price, duration, stops, and booking link

### User wants hotels
1. **Start with Skiplagged** — good hotel + flight bundles
2. **Cross-check with Trivago** — compares across booking sites
3. Present with nightly rate, total price, rating, and booking link

### User wants car rental
1. Use **Skiplagged** `sk_cars_search`

### User wants ferries
1. Use **Ferryhopper** — 33 countries, 190+ operators

### User wants "cheapest way to get from A to B"
1. Search flights on Kiwi + Skiplagged
2. Check ferries if coastal/island route
3. Compare and recommend best value (price vs time)

### User wants a full trip planned
1. Read [trip-planner.md](references/trip-planner.md) for the complete workflow
2. Gather requirements → search flights → search hotels → build budget → generate itinerary
3. Present with booking links and day-by-day plan

## Presenting Results

Use bullet lists (no markdown tables on Discord/WhatsApp). For each option show:
- Route with stops (e.g., OVD → BCN → FCO)
- Times and duration
- Price
- Booking link

Group by: 💸 Cheapest → ⚡ Fastest → 🎯 Best value

Always include booking deep links so the user can act immediately.

## Provider Endpoints

```
Kiwi:        https://mcp.kiwi.com
Skiplagged:  https://mcp.skiplagged.com/mcp
Trivago:     https://mcp.trivago.com/mcp
Ferryhopper: https://mcp.ferryhopper.com/mcp
```

## Notes
- All Tier 1 providers are free, no API key needed
- Kiwi uses `dd/mm/yyyy` date format
- Skiplagged uses `YYYY-MM-DD` date format
- Always resolve city names to IATA codes first when using Skiplagged
- Rate limit: be reasonable, don't spam requests
- MCP sessions may expire; re-initialize if you get errors
