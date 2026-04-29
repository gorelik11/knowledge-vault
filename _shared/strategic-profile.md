# Strategic Profile — Dima Gorelik

## Identity
- Dmitry (Dima) Gorelik — composer, classical/jazz guitarist, programmer
- Israeli citizen, 16+ years in Poland (Warsaw)
- 2x AICF Prize, "Outstanding Musician" Israeli Ministry of Culture
- Played with: Avishai Cohen, Trilok Gurtu, Anna Maria Jopek, Zbigniew Namyslowski, Max Roach, James Moody
- Member ZAIKS + SAWP. Website: dimagorelik.org

## Band: Kolot the Voices
- Jazz/world music, 23 original compositions
- Evolution: Dima Gorelik Trio -> Kolot the Voices (added vocalist Agata Skrzypek ~1 year ago)
- 7 countries, 7 languages in repertoire
- Track record: 3 music videos, 2 singles, 10-concert Poland tour 2025, TVP Kultura broadcast
- Lyrics: Agata Skrzypek (PL), Gorelik (Hebrew, Italian), Aniel Someillan (Spanish), traditional (Turkish, Romani)
- Featured guest: Krzysztof Scierianski (legendary Polish bassist)

## The Polish Jazz Scene Problem (CRITICAL CONTEXT)
- Polish jazz scene is extremely isolationist
- Jazz Forum (main jazz organization, controls major festivals like Jazz nad Odra) explicitly blocks Dima
- Jazz Forum director told Dima directly: "I consider you Russian, so while this depends on me, you won't perform in Poland"
- This applies to ALL Jazz Forum-connected festivals and state-linked venues
- Even Avishai Cohen (world star) is now blocked due to his own conflict
- Israeli artists barely get into Poland except at world-star level
- DeepSeek confirmed: Israeli artists (Sharon Mansur, Zohar & Adam) play Germany, NOT Poland

## Booking Strategy (Response to the Problem)
- Created independent venue database via Apify Facebook Event Scraper -> 980 hosts
- Classified: 423 VENUE + 177 ORG = 600 targets
- Scraped contacts: 1889 emails -> 426 venues with best email
- Email campaign: 133 sent, ~275 remaining (Polish language, vocative case). Updated 2026-03-22
- Strategy: bypass Jazz Forum entirely, target independent venues directly
- This approach WORKS — Dima does organize concerts this way

## Financial Reality
- Standard concert fee: 1000-2500 PLN (~250-625 EUR)
- Rare: above 2500 PLN
- Below 1000 PLN: ticket-based concerts, prefers solo/duo for those
- Krakow: many open venues but pay ~150 PLN/artist (not viable for full band)
- No point fighting closed doors (Jazz Forum). Focus on what's accessible

## Active Projects

### 1. Email Campaign (kolot_campaign/)
- Status: 133/408 sent, ~275 remaining (updated 2026-03-22)
- Script: Python, Gmail SMTP, draft mode
- Polish vocative grammar, gender detection
- GitHub: gorelik11/events-pipeline (sanitized)

### 2. Goethe-Institut IKF Grant
- Deadline: 1 April 2026 (10 DAYS AWAY)
- Amount: EUR 15,000-30,000
- Title: "Kolot - The Voices: Home"
- German co-producer: Tom Dayan (Berlin, Israeli, composer/percussionist)
- Venues: Centrum Kultury Jazovia (Gliwice), Galeria Projekt (Warsaw), Berlin TBD
- Missing: letters of intent, Tom's bio, detailed project description, finance plan
- Previous support: ZAIKS 5000 PLN (approved Dec 2025)

### 3. Other Grant Opportunities
- Visegrad Fund: EUR 25-35K, deadline 1 June 2026 (need Czech/Slovak partner)
- MKiDN "Muzyka": deadline Oct-Nov 2026 (verify foreigner eligibility)
- Musikfonds Berlin: 3001-50000 EUR (requires German residency — Tom could apply?)
- Azrieli Music Prizes: CAD 250K, next cycle 2027-2028
- NOTE: Dima is NOT a member of ACUM (Israeli). He IS a member of ZAIKS (Polish) + SAWP
- ZAIKS grant (5000 PLN) already received (approved Dec 2025) — this is done

### 4. YouTube / SEO (Social-Media/)
- Channel: @DimaGorelik
- Website: dimagorelik.org (WordPress + Elementor)
- VideoObject schema on /gallery/ (20 videos)
- Ranks #1 for "Dima Gorelik"
- Strategy: video rich results via schema markup

### 5. ReaScripts (~/ReaScripts/)
- REAPER Lua/Python scripts + JSFX plugins
- RCBit limiter series (brickwall, soft, compressor)
- Audio alignment, auto tempo map, MIDI voice splitting
- MCP integration for AI-assisted DAW control
- Monetization: NOT NOW. Free first, Patreon when revolutionary enough
- GitHub: gorelik11/ReaScripts

### 6. MIDI Composition (~/MIDI-Composition/)
- Voice splitting (piano -> string quartet)
- Jam Origin MIDI Guitar 2 for guitar->MIDI
- VSTi: CSS, Berlin Strings
- Composer harmony reference (Jarrett, Evans, Mahler, Brahms, etc.)

## Key Relationships
- Tom Dayan (Berlin) — German co-producer, crucial for Goethe grant + German market
- Agata Skrzypek — vocalist/lyricist, speaks Arabic & Hebrew
- Krzysztof Kobylinski — Jazovia director, has Goethe experience
- Noa — booking agent/manager
- Krzysztof Scierianski — bass legend, featured guest

## Competitive Landscape
- ACT Music (German label) = key for European market entry
- Fresh Sound New Talent = for new names
- German market more open to Israeli artists than Poland
- Successful models: Sharon Mansur (ACT + German clubs), Zohar & Adam (festival circuit)
- Polish successful models: Michal Tokaj (academic + artist), Rafal Sarnecki (NYC base + Culture.pl tours)

## Technical Skills
- Programming: Python, Lua, JSFX (C-like DSP), JavaScript
- Audio: mastering, bit-accurate processing, neural network beat detection
- AI/Automation: Claude Code, MCP servers, Playwright, web scraping
- SEO: schema markup, Core Web Vitals, E-E-A-T

## Strategic Advisor Agent — Usage Rules
- Run strategic-advisor via Sonnet model by default (cost-efficient)
- Use Opus only when user explicitly asks for deep analysis
- Invoke proactively after completing significant tasks in any project
- Agent reads this file for context — keep it updated after key events
- Market research data: /Volumes/KINGSTON/JazzData.md

## Goethe Grant Status (update as things change)
- Email to Goethe Warsaw: SENT, they confirmed receipt (phone call)
- Waiting for: approval/contact person from Warsaw office (1 week silence so far)
- Cannot submit portal application until Warsaw office confirms
- Deadline: 1 April 2026
