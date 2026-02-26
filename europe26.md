# Claude Code Prompt: Build "Alps to Tuscany" Trip Hub

Build a single-file **interactive trip hub** for our family road trip (March 23 – April 2). This is NOT a brochure — it's a living tool we'll use every day on the ground. Think of it like a personal travel command center on your phone: today's plan at a glance, notes you jot down at dinner, a checklist of what to pack, expenses you log at the hotel. Everything persists in localStorage so it survives refreshes and works offline-ish.

**The core idea**: open this on your phone at breakfast, see today's plan instantly, tap to see destinations/hotels, jot a note ("that restaurant in Pienza was incredible — get the truffle pasta"), check off a packing item, log what you spent. Next morning, repeat.

## Tech Stack
- Single `index.html` file — HTML + CSS + vanilla JS (no React, no build step)
- Tailwind CSS via CDN
- Google Fonts: pick a distinctive serif + sans pairing (NOT Inter/Roboto — try DM Serif Display + DM Sans, or Fraunces + Outfit, or something with personality)
- ALL user data persists in `localStorage` (notes, checklists, expenses, dark mode preference)
- Deploy-ready for Netlify (drag and drop)

---

## Design Vision: "Travel Journal App Meets Luxury Guide"

### Aesthetic Direction
- **NOT generic AI slop.** This should feel like a hand-crafted travel journal with app-like interactivity
- Color-code by country phase:
  - 🇦🇹 Austria days (1-4): Deep alpine teal/emerald gradients, cool mountain feel
  - 🚗 Transition day (5): Warm amber/gold gradient — the pivot from Alps to Tuscany
  - 🇮🇹 Italy days (6-10): Terracotta, burnt sienna, Tuscan gold — warm Mediterranean
  - ✈️ Departure (11): Cool slate — winding down
- CSS gradients, subtle texture overlays, glassmorphism for depth — no flat boring cards
- Emoji as functional icons (not decoration) — 🏔☀️🌙🛏🚗🚦👨‍👩‍👧‍👦⭐📝✅💶
- Animated floating route path in the hero (🏔 → 🌻 → 🏛 → ✈️)
- Smooth reveal animations (CSS `@keyframes`, not heavy JS libraries)
- Bottom tab bar for hub navigation (like a native app)

### Typography
- Display headings: characterful serif (luxury travel feel)
- Body text: clean geometric sans (phone readability)
- Minimum 16px body, generous line-height (1.6+)

---

## App Structure: Bottom Tab Navigation

The hub has **4 main views** controlled by a sticky bottom tab bar (like iOS/Android apps):

### Tab 1: 📅 Today (default view)
- **Auto-detects current date** and shows today's day card fully expanded
- If outside trip dates (before Mar 23 or after Apr 2), shows Day 1 with a countdown or Day 11 with a "Trip complete!" message
- Quick-glance header: day number, date, flag, title
- Full day content always visible (no collapsing needed for Today view):
  - AM/PM plans
  - Sleep location
  - Parking + ZTL status badges
  - 👨‍👩‍👧‍👦 Family Tip
  - Destinations with links
  - Hotel picks (if applicable)
- **Today's Notes** section at the bottom — textarea to jot quick notes for today (persists in localStorage per day)

### Tab 2: 🗺 All Days (scrollable itinerary)
- The full 11-day itinerary with collapsible day cards
- Sticky horizontal day nav at top (scrollable tabs, color-coded by phase)
- IntersectionObserver tracks active day as you scroll
- Each day card:
  - **Collapsed default**: gradient header with day number, title, flag, AM/PM, sleep
  - **Tap to expand**: status badges, family tip, destinations, hotels, day-specific notes
  - Chevron rotates on expand/collapse
  - Smooth slideDown animation

### Tab 3: 📝 Notes & Lists
A dedicated space for trip notes, packing checklists, and expense tracking. Three sub-sections accessible via horizontal toggle pills at the top:

#### 📝 Trip Journal
- A running list of notes with timestamps
- "Add Note" button opens a modal/inline form with:
  - Text area for the note
  - Optional day tag dropdown (Day 1-11 or "General")
  - Save button
- Notes display as cards in reverse chronological order (newest first)
- Each note shows: text, timestamp, day tag (if any)
- Swipe-left or tap trash icon to delete a note (with confirmation)
- All notes persist in localStorage
- **Pre-populated with one example**: "✈️ Trip starts Mar 23! Don't forget to download offline maps for Austria & Italy."

#### ✅ Checklists
- Multiple checklists with add/remove functionality
- **Pre-loaded checklists**:

**🧳 Packing List:**
- [ ] Passports (all family members)
- [ ] EU power adapters (2x)
- [ ] Car phone mount
- [ ] Kids' tablets + headphones
- [ ] Download offline Google Maps (Austria + Italy)
- [ ] Snacks for Day 5 big drive
- [ ] Comfort items for kids (stuffed animals, blankets)
- [ ] Sunscreen + hats
- [ ] Comfortable walking shoes (everyone)
- [ ] Rain jackets (March weather!)
- [ ] Camera / phone charger / portable battery
- [ ] Printed hotel confirmations (backup)
- [ ] International driving permit (if needed)
- [ ] Travel insurance docs
- [ ] Kids' activity bag for flights

**📋 Pre-Trip To-Do:**
- [ ] Book Salzburg hotel
- [ ] Book Val d'Orcia hotel
- [ ] Book Verona hotel
- [ ] Book Florence airport hotel
- [ ] Reserve rental car (Munich pickup → Florence drop-off)
- [ ] Buy Austria Vignette (motorway sticker) online
- [ ] Download offline maps
- [ ] Notify bank of travel dates
- [ ] Check Arena di Verona hours (March closures?)
- [ ] Pack kids' entertainment for flights + drives
- [ ] Confirm Das Edelweiss reservation

**🇮🇹 ZTL Survival Checklist:**
- [ ] Read ZTL rules before entering Italy
- [ ] Download ZTL map for Florence
- [ ] Confirm Verona hotel is OUTSIDE ZTL
- [ ] Confirm Florence hotel is OUTSIDE ZTL
- [ ] Set GPS to "avoid city centers" in Italy
- [ ] Save Parcheggio Cittadella (Verona) address in Maps
- [ ] DO NOT follow GPS into walled Tuscan towns

- Users can add new items to any checklist
- Users can create entirely new checklists (e.g., "Shopping List", "Restaurants to Try")
- Check/uncheck with tap (satisfying checkbox animation)
- Progress bar shows completion % per checklist
- All state persists in localStorage

#### 💶 Expenses
- Simple expense tracker to log daily spending
- "Add Expense" form:
  - Amount (number input with € symbol)
  - Category dropdown: 🍽 Food | 🏨 Hotel | ⛽ Gas | 🎫 Tickets | 🛍 Shopping | 🚗 Parking | 📱 Other
  - Optional note (short text)
  - Day auto-tagged to current trip day (editable)
- Expense list shows each entry as a compact row
- **Summary view** at top:
  - Total spent (running sum)
  - Breakdown by category (small horizontal bar chart or pill badges)
  - Per-day average
- Tap an expense to edit or delete
- All expenses persist in localStorage
- **Export button**: copies a clean text summary to clipboard (for pasting into a spreadsheet later)

### Tab 4: ⚙️ Settings
- 🌙 Dark Mode toggle (persists in localStorage)
- 🚦 ZTL Quick Reference panel (always accessible from here too)
- 🗑 Clear All Data button (with "Are you sure?" confirmation — clears notes, expenses, checklists)
- 📋 Export All Data button (copies everything to clipboard as JSON — backup)
- ℹ️ Trip summary stats (11 days, 5 hotels, 2 countries, etc.)

---

## Interactive Features (ALL REQUIRED)

### 1. Bottom Tab Bar (Primary Navigation)
- Fixed to bottom of viewport (like a native app)
- 4 tabs: 📅 Today | 🗺 Days | 📝 Notes | ⚙️ Settings
- Active tab highlighted with phase color
- Respects iPhone safe areas (`env(safe-area-inset-bottom)`)
- Slight shadow/blur effect on top edge

### 2. Sticky Day Navigation (inside "All Days" tab)
- Horizontal scrollable tabs pinned below the bottom tab bar content area
- Color-coded by phase
- Active day auto-highlights via IntersectionObserver
- Tap to smooth-scroll

### 3. Collapsible Day Cards
- Collapsed default: gradient header + summary
- Expand: full content + per-day notes area
- Smooth animations
- Chevron rotation

### 4. Dark Mode
- Toggle in Settings tab AND in the top-right corner (always accessible)
- Full theme switch — all backgrounds, cards, text, badges, modals
- Persists via localStorage
- Essential for nighttime hotel use

### 5. ZTL Warning System
- Accessible from Settings tab
- Also shows as a persistent amber/red banner on Day 5+ cards (Italy days)
- Red-tinted panel with country-by-country rules
- Fine amounts prominently displayed
- Links to official ZTL maps

### 6. localStorage Persistence
- **Everything user-generated persists**: notes, checklists, expenses, dark mode, which cards are expanded
- Use a single `TRIP_HUB_DATA` key in localStorage with a structured JSON object
- On page load, hydrate all state from localStorage
- On any state change, debounce-save to localStorage (200ms)
- Data structure:
```json
{
  "version": 1,
  "darkMode": false,
  "notes": [{ "id": "...", "text": "...", "day": 3, "timestamp": "..." }],
  "checklists": {
    "packing": { "title": "🧳 Packing List", "items": [{ "text": "Passports", "checked": false }] },
    "pretip": { "title": "📋 Pre-Trip To-Do", "items": [...] },
    "ztl": { "title": "🇮🇹 ZTL Survival", "items": [...] }
  },
  "expenses": [{ "id": "...", "amount": 45.50, "category": "food", "note": "Dinner in Pienza", "day": 6, "timestamp": "..." }],
  "expandedDays": [1, 5]
}
```

### 7. Family Tip Highlights
- Every day has a 👨‍👩‍👧‍👦 Family Tip box (pink/rose tint)
- These feel like insider tips from a friend, not guidebook filler
- Prominent and unmissable

### 8. Hotel Cards
- Inside expanded day cards, behind a "🏨 Hotel Picks" toggle
- Each card: name, description, parking, price (€ symbols), family perk
- "View →" button links to hotel website
- Subtle lift on tap

### 9. Destination Cards
- Tappable, link out to official websites (new tab)
- ⭐ badge for especially family-friendly spots
- Short, punchy descriptions

---

## Mobile-First Requirements (NON-NEGOTIABLE)

This is a phone app used one-handed in European cities and moving cars.

- `<meta name="viewport" content="width=device-width, initial-scale=1">`
- All tap targets min 44x44px with 8px spacing
- No horizontal scroll anywhere
- No hover-only interactions
- Bottom tab bar within iPhone safe areas
- `font-display: swap` on all fonts
- `scroll-behavior: smooth` with `prefers-reduced-motion` respect
- Fast loading: < 3 seconds on European 4G
- Content readable even if CSS fails (semantic HTML)
- Modals/forms must work well on mobile keyboards (input types, autofocus, no viewport jump)

---

## FULL ITINERARY DATA

### Hero Section
- Title: **"Alps to Tuscany"**
- Subtitle: "Family Trip Hub"
- Route: Munich → Salzburg → Grossarl → Val d'Orcia → Verona → Florence
- Dates: March 23 – April 2
- Stats: 11 Days · 5 Hotels · 2 Countries
- Animated route: 🏔 → 🌻 → 🏛 → ✈️ (gentle float animation)

---

### DAY 1 — Mar 23 (Sun) 🇦🇹 — "Arrival → Salzburg"
- **Phase**: austria
- ☀️ AM: Land Munich (11 AM) → Pick up rental car → 1.5 hr scenic drive to Salzburg
- 🌙 PM: Salzburg Old Town stroll + early family dinner
- 🛏 Sleep: Salzburg (🏰)
- 🚗 Parking: ⚠️ Hotel garage required
- 🚦 ZTL: ⚠️ Some central areas restricted — confirm hotel access
- 👨‍👩‍👧‍👦 Family Tip: "Old Town is compact & flat — perfect evening stroll after a long flight. Kids will love the golden sphere sculpture in Kapitelplatz and the funicular up to the fortress!"

**Destinations:**
- ⭐ [Hohensalzburg Fortress](https://www.salzburg.info/en/sights/top10/hohensalzburg-fortress) — Largest medieval fortress in Europe! Take the funicular up — kids love the ride. Knight's rooms & puppet museum inside.
- ⭐ [Getreidegasse](https://www.salzburg.info/en/sights/top10/getreidegasse) — Fairy-tale shopping lane with wrought-iron signs. Mozart's Birthplace at #9. Get Mozartkugeln (chocolate balls) for the kids!
- ⭐ [Mirabell Palace & Gardens](https://www.salzburg.info/en/sights/top10/mirabell-palace-gardens) — Sound of Music filming location! Kids can run through the Do-Re-Mi gardens. Dwarf Garden is wonderfully weird.
- [Salzburg Cathedral](https://www.salzburg.info/en/sights/top10/salzburg-cathedral) — Baroque masterpiece where Mozart was baptized. Free to enter.
- [Residenzplatz](https://www.salzburg.info/en/sights/top10/residenz) — Heart of Old Town with Salzburg's most beautiful fountain.

**Hotels:**
| Name | Why | Parking | Price | Family Perk |
|------|-----|---------|-------|-------------|
| [Hotel Sacher Salzburg](https://www.sacher.com/hotel-sacher-salzburg/) | Grand historic luxury on the Salzach River. Famous Sacher Torte — kids will devour it! | Valet available | €€€€ | Spacious rooms, riverside views |
| [Sheraton Grand Salzburg](https://www.marriott.com/hotels/travel/szggs-sheraton-grand-salzburg/) | Best for families — large indoor pool, multiple restaurants, rooms with sofa beds. | Hotel garage | €€€ | Indoor pool, kids menu, sofa beds |
| [Hotel Bristol Salzburg](https://www.bristolsalzburg.at/en/) | Family-run 3 generations, 5-star, steps from Mirabell Palace. Award-winning restaurant. | Garage ~300m (~€30/night) | €€€ | Central location, elegant rooms |

---

### DAY 2 — Mar 24 (Mon) 🏔 — "Grossarl Check-in"
- **Phase**: austria
- ☀️ AM: Breakfast in Salzburg → 1 hr drive to Grossarl Valley
- 🌙 PM: Check-in at Das Edelweiss → Spa, waterpark & pool time!
- 🛏 Sleep: Das Edelweiss (1/3) (⛷)
- 🚗 Parking: ✅ Free resort parking
- 🚦 ZTL: ✅ No ZTL
- 👨‍👩‍👧‍👦 Family Tip: "The indoor waterpark has 5 SLIDES and a warm toddler pool. Four age-specific kids clubs mean parents can hit the spa guilt-free!"

**Destinations:**
- ⭐ [Das Edelweiss Resort](https://www.edelweiss-grossarl.com/en/) — 5-star family resort, Michelin 2 Keys. 7,000m² Mountain Spa with family & adults-only zones.
- ⭐ Indoor Waterpark — 5 water slides, toddler pool, lazy river — kids won't want to leave!
- Mountain Cuisine — Steak at Sirloin Grill & Dine, sushi at Sakura, or pizza at Cantina & Pizza Inferno.

**Hotels:**
| Name | Why | Parking | Price | Family Perk |
|------|-----|---------|-------|-------------|
| [Das Edelweiss Mountain Resort](https://www.edelweiss-grossarl.com/en/) | 5-star, 3rd generation family-run. Michelin 2 Keys. Indoor waterpark, 4 kids clubs, mountain spa. | Free on-site | €€€€ | Waterpark, 4 kids clubs by age, pizza restaurant |

---

### DAY 3 — Mar 25 (Tue) 🏔 — "Alpine Adventure Day"
- **Phase**: austria
- ☀️ AM: Cable car ride up Panoramabahn → Alpine walk or valley exploration
- 🌙 PM: Mountain dinner at the resort + evening swim
- 🛏 Sleep: Das Edelweiss (2/3) (⛷)
- 🚗 Parking: ✅ Car stays parked
- 🚦 ZTL: ✅ No ZTL
- 👨‍👩‍👧‍👦 Family Tip: "Take the Panoramabahn cable car right from the hotel — stunning views! 40+ traditional mountain huts serve hot chocolate and strudel. Guided family walks available."

**Destinations:**
- ⭐ [Panoramabahn Cable Car](https://www.grossarltal.info/en/) — Steps from hotel! Ride up for panoramic valley views. Spring hiking or snow play.
- ⭐ [Grossarl Valley Almen](https://www.grossarltal.info/en/) — 40+ traditional alpine huts — hot chocolate, apple strudel & Kaiserschmarrn (fluffy shredded pancakes!).

---

### DAY 4 — Mar 26 (Wed) 🏔 — "Relax or Explore"
- **Phase**: austria
- ☀️ AM: Slow mountain morning OR half-day Salzburg trip
- 🌙 PM: Final spa evening — soak it all in
- 🛏 Sleep: Das Edelweiss (3/3) (⛷)
- 🚗 Parking: ✅ Easy village parking
- 🚦 ZTL: ✅ No ZTL
- 👨‍👩‍👧‍👦 Family Tip: "Option A: Full kids club + spa day for parents. Option B: Hellbrunn Palace has trick water fountains that spray unsuspecting visitors — kids LOVE it (30 min drive)."

**Destinations:**
- ⭐ [Hellbrunn Palace](https://www.hellbrunn.at/en) — 30 min from resort. Trick water fountains — kids will be in hysterics! Sound of Music gazebo too.
- ⭐ Resort Spa Day — Last chance for waterpark, infinity pool & mountain views.

---

### DAY 5 — Mar 27 (Thu) 🚗 — "Alps to Tuscany" ⭐ Big Drive Day
- **Phase**: transition
- ☀️ AM: Scenic 5 hr drive south → Coffee stop in Innsbruck + Brenner Pass into Italy
- 🌙 PM: Arrive Val d'Orcia — Tuscan countryside welcome!
- 🛏 Sleep: Val d'Orcia (1/3) (🌻)
- 🚗 Parking: ✅ On-site estate parking
- 🚦 ZTL: ✅ Stay outside towns — no issues
- 👨‍👩‍👧‍👦 Family Tip: "Big drive day! Pack snacks, download movies, bring coloring books. Innsbruck coffee stop breaks it up. Brenner Pass is exciting — you're crossing the Alps! Let kids spot the Italy border signs."

**Drive Route:**
- Grossarl → Innsbruck (~2 hrs): Scenic motorway through alpine valleys
- [Innsbruck Old Town](https://www.innsbruck.info/en/) — Quick coffee & leg stretch. Golden Roof fun to spot.
- Innsbruck → Brenner Pass (~30 min): Cross into Italy!
- Brenner → Val d'Orcia (~4 hrs): A22 south through Trentino, A1 toward Siena
- **Total: ~5 hours driving + stops**

**Destinations:**
- ⭐ [Innsbruck Old Town](https://www.innsbruck.info/en/) — Quick coffee & leg stretch. Golden Roof (Goldenes Dachl). Mountains tower over the city!
- [Val d'Orcia UNESCO Site](https://www.italia.it/en/tuscany/things-to-do/val-orcia) — Rolling hills, cypress trees, medieval villages.

**Hotels:**
| Name | Why | Parking | Price | Family Perk |
|------|-----|---------|-------|-------------|
| [Rosewood Castiglion del Bosco](https://www.rosewoodhotels.com/en/castiglion-del-bosco) | Ultra-luxury Tuscan resort. Vineyards, spa, golf, stunning suites. | Free estate parking | €€€€€ | Kids programs, pool, cooking classes |
| [Adler Thermae Spa Resort](https://www.adler-thermae.com/en/) | Luxury thermal spa in Bagno Vignoni. Central Val d'Orcia. | Free on-site | €€€€ | Thermal pools, kids activities |
| [Tenuta Santo Pietro](https://www.tenutasantopietro.com/) | Family-friendly luxury agriturismo. Cooking classes, truffle hunting! | Free on-site | €€€ | Cooking classes, farm animals, truffle hunts |
| [Castello Banfi – Il Borgo](https://www.castellobanfiwineresort.it/en/) | Relais & Chateaux wine estate near Montalcino. Historic castle. | Estate parking | €€€€ | Castle tours, vineyard walks |
| [L'Olmo](https://www.olmopienza.it/) | Boutique 4-star just outside Pienza, only 8 rooms. Pool, rolling fields. | Free on-site | €€€ | Intimate, quiet, pool |

---

### DAY 6 — Mar 28 (Fri) 🇮🇹 — "Pienza & Montepulciano"
- **Phase**: italy
- ☀️ AM: Pienza — cheese tasting, Renaissance streets, panoramic views
- 🌙 PM: Montepulciano — tower climb + vineyard dinner
- 🛏 Sleep: Val d'Orcia (2/3) (🌻)
- 🚗 Parking: ⚠️ Park OUTSIDE town walls
- 🚦 ZTL: ⚠️ Do NOT drive into historic town centers!
- 👨‍👩‍👧‍👦 Family Tip: "Pienza's pecorino cheese shops have free samples everywhere! In Montepulciano, climb the Palazzo Comunale tower for a 360° view. Streets named 'Love', 'Kiss' and 'Good Luck'!"

**Destinations:**
- ⭐ [Pienza](https://www.discovertuscany.com/pienza/) — The "Ideal Renaissance City" — pecorino cheese capital! Walk behind the cathedral for jaw-dropping views.
- ⭐ [Montepulciano](https://www.discovertuscany.com/montepulciano/) — Medieval hilltop town. Climb Palazzo Comunale tower for 360° views. Caffè Poliziano panoramic terrace.
- Ristorante Daria (Monticchiello) — Authentic Tuscan dishes. Book ahead!
- Il Rossellino (Pienza) — Traditional cooking in charming piazza.
- La Bandita Townhouse (Pienza) — Modern Tuscan with international twists.

---

### DAY 7 — Mar 29 (Sat) 🇮🇹 — "Tuscan Slow Day"
- **Phase**: italy
- ☀️ AM: Farm visit or countryside drive — gelato stops mandatory
- 🌙 PM: Sunset dinner with Val d'Orcia views
- 🛏 Sleep: Val d'Orcia (3/3) (🌻)
- 🚗 Parking: ✅ No driving needed from estate
- 🚦 ZTL: ✅ No issues from countryside
- 👨‍👩‍👧‍👦 Family Tip: "Visit Podere il Casale — kids can meet 1,000+ sheep and watch pecorino cheese being made! Bagno Vignoni has a Roman thermal pool in the town square — surreal."

**Destinations:**
- ⭐ [Montalcino](https://www.discovertuscany.com/montalcino/) — City of Brunello wine. Climb the 14th-century fortress — wine tasting inside (grape juice for kids!).
- ⭐ Vitaleta Chapel — THE iconic Tuscan photo — tiny white church on a hill between cypress trees.
- Bagno Vignoni — Ancient Roman thermal pool in the town square! Steaming water fascinates kids.
- [Podere il Casale](https://www.discovertuscany.com/valdorcia/) — Farm with 1,000+ sheep — watch pecorino being made! Picnic with views.
- San Quirico d'Orcia — Romanesque church, Horti Leonini Renaissance gardens.

---

### DAY 8 — Mar 30 (Sun) 🇮🇹 — "Verona — Romeo & Juliet City"
- **Phase**: italy
- ☀️ AM: 2.5–3 hr drive Val d'Orcia → Verona
- 🌙 PM: Arena di Verona (older than the Colosseum!) + Piazza evening stroll
- 🛏 Sleep: Verona — OUTSIDE ZTL (🏛)
- 🚗 Parking: ⚠️ Hotel garage OUTSIDE old town — critical!
- 🚦 ZTL: ⚠️ Stay OUTSIDE ZTL zone — walk into old town
- 👨‍👩‍👧‍👦 Family Tip: "The Arena held gladiator fights and 30,000 spectators — it's like a smaller Colosseum! Under 8s are FREE. Visit Juliet's balcony for the photo op. Secret: Roman ruins hide in the Benetton store basement on Via Mazzini!"

**Destinations:**
- ⭐ [Arena di Verona](https://arenaverona.org/en) — 1st century AD — best preserved amphitheater in the world! Adults ~€12, kids under 8 FREE.
- ⭐ [Juliet's House](https://www.visitverona.it/en) — The famous balcony! Touch Juliet's statue for luck.
- ⭐ [Piazza delle Erbe](https://www.visitverona.it/en) — Ancient Roman forum turned lively market. Gelato & frescoed buildings.
- [Piazza Bra](https://www.arena.it/en/arena-verona-opera-festival/get-ready-for-the-opera/visiting-verona/) — Grand main square, cafés along the "Liston" promenade.
- Lamberti Tower — Tallest in Verona — amazing views. Kids love the climb.

**Parking strategy**: Corso Porta Nuova from the south — NOT in ZTL. Park at Parcheggio Cittadella (underground, modern) — 2-3 min walk to Arena, zero ZTL risk.

**Hotels (ALL outside ZTL):**
| Name | Why | Parking | Price | Family Perk |
|------|-----|---------|-------|-------------|
| [Hotel Indigo Verona](https://www.ihg.com/hotelindigo/hotels/us/en/verona/vrnin/hoteldetail) | Elegant 1920s Liberty-style. 10-min walk to Arena. | Available, outside ZTL | €€€ | Walkable, stylish rooms |
| [Best Western CTC Verona](https://www.bwctchotelverona.it/en/) | Spacious rooms, free shuttle to center. Ample parking. | Free ample parking | €€€ | Free shuttle, restaurant |
| [Relais Villa dei Gelsi & Spa](https://www.villadeigelsi.com/) | Luxury farmstay with pool, spa, indoor pool. 1.5 km from center. | Free private parking | €€€ | Pool, spa, family rooms |

---

### DAY 9 — Mar 31 (Mon) 🇮🇹 — "Verona → Florence Area"
- **Phase**: italy
- ☀️ AM: Morning Verona stroll — last gelato!
- 🌙 PM: 2.5 hr drive to Florence airport area
- 🛏 Sleep: Florence Airport Hotel (✈️)
- 🚗 Parking: ✅ Airport hotel parking
- 🚦 ZTL: ✅ No ZTL near airport
- 👨‍👩‍👧‍👦 Family Tip: "Let the kids pick one last Verona treat (gelato, obviously). Highway drive = good nap time. DON'T go into Florence city center with the car!"

**Hotels (near airport, OUTSIDE ZTL):**
| Name | Why | Parking | Price | Family Perk |
|------|-----|---------|-------|-------------|
| [Hilton Garden Inn Florence Novoli](https://www.hilton.com/en/hotels/flrfigi-hilton-garden-inn-florence-novoli/) | Modern, near airport. Tram to Florence center. | Free self-parking | €€ | Restaurant, tram to city |
| [Villa Campestri Olive Oil Resort](https://www.villacampestri.com/en/) | Final splurge! 5-star olive oil estate. Pool, spa, incredible breakfast. | Free on-site | €€€€ | Pool, farm, stunning grounds |
| [Starhotels Tuscany](https://www.starhotels.com/en/our-hotels/tuscany-florence/) | 4-star, tram stop right in front — direct to city center. | Self-parking | €€€ | Tram access, restaurant |

---

### DAY 10 — Apr 1 (Tue) 📦 — "Buffer Day — Relax & Pack"
- **Phase**: italy
- ☀️ AM: Sleep in! Buffer morning. Kids play at hotel.
- 🌙 PM: Relaxed final Italian dinner — no rush
- 🛏 Sleep: Florence Airport Hotel (✈️)
- 🚗 Parking: ✅ Hotel parking
- 🚦 ZTL: ✅ No ZTL
- 👨‍👩‍👧‍👦 Family Tip: "This is YOUR day. Let kids swim, do laundry, pack calmly. One last pizza. Set out tomorrow's travel clothes tonight!"

---

### DAY 11 — Apr 2 (Wed) ✈️ — "Fly Home!"
- **Phase**: departure
- ☀️ AM: Early departure — 6:30 AM flight. Return rental car at Florence Airport.
- 🌙 PM: —
- 🛏 Sleep: Home sweet home (🏠)
- 🚗 Parking: ✅ Return car at airport
- 🚦 ZTL: —
- 👨‍👩‍👧‍👦 Family Tip: "Pack a small activity bag in carry-on for the flight. Download shows the night before. Airport snack haul is a fun tradition to start!"

---

## ZTL Quick Reference Data (for Settings tab panel)

| Region | Status | Rule |
|--------|--------|------|
| 🇦🇹 Austria | ✅ | No ZTL — drive freely |
| 🇮🇹 Tuscany Towns | ⚠️ | NEVER drive inside walled town centers |
| 🇮🇹 Verona | ⚠️ | Stay outside old town. Park at Cittadella garage. |
| 🇮🇹 Florence | 🛑 | DO NOT enter city center. Airport area only! |

**Fine alert**: €80–€335 PER camera entry + €45 rental car admin fee. Cameras automatic. Fines arrive 6-12 months later. GPS does NOT warn you!

**Links:**
- [Florence ZTL Map](https://www.visitflorence.com/tourist-info/driving-in-florence-ztl-zone.html)
- [Italy ZTL Guide](https://mominitaly.com/ztl-in-italy/)
- [Auto Europe ZTL Maps](https://www.autoeurope.com/italy-ztl-zones/)

---

## Implementation Notes

### Structure
```
/
├── index.html    (everything — HTML, inline <style>, inline <script>)
```

### Key Technical Requirements
- Bottom tab navigation as primary app structure (not page scroll)
- Each tab is a view/panel — only one visible at a time
- All user data in a single `localStorage` key (`TRIP_HUB_DATA`) as JSON
- Debounced saves (200ms) on every state change
- IntersectionObserver for active day in the Days tab
- CSS `@keyframes` for animations (slideDown, float, fadeIn)
- All external links: `target="_blank" rel="noopener noreferrer"`
- Tailwind responsive: default = mobile, `md:` = tablet, `lg:` = desktop
- No images — emoji + CSS gradients for visual flair
- Itinerary data hardcoded in a JS array at top of script

### localStorage Schema
```json
{
  "version": 1,
  "darkMode": false,
  "notes": [],
  "checklists": {},
  "expenses": [],
  "expandedDays": [],
  "activeTab": "today"
}
```
On first load, if no data exists, initialize with pre-loaded checklists and the example note. On subsequent loads, hydrate from stored data. Always merge — never overwrite user data with defaults.

### Performance
- Target: < 3 seconds on European 4G
- Only 2 external resources: Tailwind CDN + Google Fonts
- Everything else inline
- `font-display: swap`

### The Vibe Check
Before you ship it, ask yourself:
1. Can I open this at breakfast and see today's plan in under 2 seconds?
2. Can I jot a note about a restaurant in 3 taps?
3. Can I check off a packing item with one tap?
4. Is the ZTL warning impossible to miss on Italy days?
5. Does every day make me think "the kids will LOVE this"?
6. Does the expense tracker actually work — add, view summary, export?
7. If I close the browser and reopen, is everything still there?

If yes to all seven — ship it. ✈️
