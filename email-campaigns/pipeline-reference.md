# Events Pipeline — Email Campaign System for Venue Booking

A complete email outreach pipeline for booking concert venues. Built for Kolot the Voices (jazz/world music band) touring in Poland, but designed to be reusable for any campaign via JSON config.

## Pipeline Overview

The system automates venue discovery, contact research, and personalized email outreach:

1. **Scrape Facebook events** → extract hosts/venues by keyword
2. **Classify venues** → VENUE / ORG / MUSICIAN / NOISE
3. **Find contact emails** → DuckDuckGo web search + contact page scraping
4. **Prioritize emails** → booking@ > director@ > info@ (scoring system)
5. **Create personalized emails** → Polish grammar (vocative case, gender detection)
6. **Create Gmail drafts** → via IMAP (user reviews before sending)
7. **Schedule drafts** → via Selenium + Firefox "Schedule Send" UI

## Scripts

### campaign.py — Universal Campaign Script

The main script, config-driven for reusability across campaigns:

```bash
python3 campaign.py --config kolot_pl.json status|preview|draft|send [--limit N]
python3 campaign.py init new_campaign_name   # Create new campaign structure
```

**Features:**
- JSON config (SMTP, sender, paths, venue keywords)
- Language pack (`lang/*.json`) — names, vocative, greetings, venue keywords
- Email templates (`templates/*.txt` and `.html`)
- Venue type detection (name keywords → email signal → category → fallback)
- Red flag system (warns when venue name vs. category mismatch)
- Decisions logging (`decisions_log.csv`)
- New campaign = new config + new templates, **zero code changes**

**Commands:**
- `status` — show sent/remaining count
- `preview` — show next N emails (no save)
- `draft` — save N emails as Gmail drafts (user reviews before sending)
- `send` — send N emails directly (manual "yes" confirmation required)

### schedule_drafts.py — Gmail Schedule Send via Selenium

Automates scheduling Gmail drafts across weekdays:

```bash
python3 schedule_drafts.py --dry-run                    # Preview schedule
python3 schedule_drafts.py --per-day 30 --time 08:30    # Schedule 30/day at 8:30 CET
```

**Features:**
- Opens Gmail drafts in Firefox
- Clicks "Schedule Send" button for each draft
- Distributes across weekdays (avoid weekends)
- 2-minute intervals between emails
- Re-authenticates between batches to avoid rate limiting

**Requirements:**
- Firefox with profile at: `~/Library/Application Support/Firefox/Profiles/[PROFILE_ID]/`
- geckodriver 0.30.0 (for macOS High Sierra compatibility)
- `caffeinate -d` to prevent system sleep during automation

### email_campaign.py — Legacy Script

Original hardcoded Polish version. Kept as backup for reference — use `campaign.py` for new work.

### find_contacts.py — Contact Scraper

DuckDuckGo search → website discovery → contact page scraping:

```bash
python3 find_contacts.py --input venues.csv --output contacts.csv
```

## Setup

### 1. Prepare Configuration

```bash
# Copy example config
cp kolot_pl.example.json kolot_pl.json

# Edit with your SMTP credentials
# Required fields:
# - smtp_server, smtp_port, login_email, app_password
# - sender_name, sender_email, send_as_email
# - contacts_file, progress_file, log_file
# - template_name, venue_lines
```

### 2. Prepare Contacts CSV

Create a CSV file with columns:
- `venue_name` — venue name
- `classification` — VENUE / ORG / MUSICIAN / NOISE
- `best_email` — prioritized contact email
- `person_name` — contact name (optional, for vocative case)
- `role_context` — job title/role (optional, for customization)
- `score` — email quality (100=booking@, 90=artistic, 80=director, 60=marketing, 40=other)
- `website` — venue website (optional)
- `all_emails` — all discovered emails (semicolon-separated, optional)

Example:
```csv
venue_name,classification,best_email,person_name,role_context,score,website,all_emails
Jazz Club Kraków,VENUE,koncerty@jazzclub.pl,Katarzyna,booking manager,100,jazzclub.pl,imprezy@jazzclub.pl;kontakt@jazzclub.pl
Filharmonia Poznańska,ORG,events@filharmonia.pl,Piotr,events director,90,filharmonia.pl,info@filharmonia.pl
```

### 3. Create Language Pack and Templates

**Language pack** (`lang/pl.json`):
```json
{
  "names": {
    "female_first": ["Anna", "Barbara", "Katarzyna", ...],
    "male_first": ["Jan", "Piotr", "Stanisław", ...],
    "name_regex": "^[A-ZĄĆĘŁŃÓŚŹŻ][a-ząćęłńóśźż]+$"
  },
  "vocative": {
    "Anna": "Anno",
    "Piotr": "Piotrze",
    ...
  },
  "greetings": {
    "fallback": "Szanowni Państwo!",
    "female": "Szanowna Pani {vocative}!",
    "male": "Szanowny Panie {vocative}!"
  },
  "venue_keywords": {
    "festival": ["festiwal", "festival"],
    "club": ["klub", "bar", "lounge"],
    "institution": ["filharmonia", "teatr", "opera"],
    "organization": ["organizacja", "stowarzyszenie", "fundacja"]
  }
}
```

**Email template** (`templates/kolot_pl.txt`):
```
Subject: Kolot the Voices — Propozycja koncertu

{greeting}

Kolot the Voices to międzynarodowy kwartet jazzowy grający muzykę {venue_line}.

Chcielibyśmy zaproponować koncert dla Waszej publiczności.

{press_url}

Pozdrawiam,
{sender_name}
{sender_phone}
```

### 4. Run Campaign

```bash
# Check status
python3 campaign.py --config kolot_pl.json status

# Preview next 5 emails
python3 campaign.py --config kolot_pl.json preview --limit 5

# Create 10 Gmail drafts (user reviews before sending)
python3 campaign.py --config kolot_pl.json draft --limit 10

# Send 10 emails (requires manual "yes" confirmation)
python3 campaign.py --config kolot_pl.json send --limit 10
```

## Selenium Scheduling

### Gmail Closure Library Limitations

The Gmail UI uses Google Closure Library, which is hardened against automation:

- **Problem:** `.click()`, JS click, and mousedown events don't trigger the "Schedule Send" dropdown
- **Solution:** Use `ActionChains.move_to_element_with_offset()` to simulate actual mouse movement
- **Send button:** `div.aoO` with offset `width // 2 + 12` pixels right

```python
send_btn = driver.find_element(By.CSS_SELECTOR, "div.aoO")
actions = ActionChains(driver)
offset = (send_btn.size['width'] // 2 + 12, 0)
actions.move_to_element_with_offset(send_btn, *offset).perform()
```

### Google Rate Limiting

- **Problem:** Google blocks after ~40-50 automated actions per session, even if scheduling different dates
- **Solution:** Limit to 40 per session, re-login Firefox between batches
- Scheduling is NOT a rate-limit bypass — Google still counts it as automation

### macOS Specifics

- **geckodriver 0.30.0 required** for High Sierra (newer versions don't work)
- **`caffeinate -d` required** to prevent system sleep during automation
  - Without it: Mac goes to sleep, Firefox window minimizes, compose crashes with `MoveTargetOutOfBounds`
- **Maximize window** before compose operations (ensures buttons are visible)
- Firefox profile copy may trigger Google re-authentication

## Known Issues & Workarounds

| Issue | Solution |
|-------|----------|
| IMAP drafts don't show To field in Gmail compose | Add `\Draft` flag via `imap.append('[Gmail]/Drafts', flags='\\Draft')` |
| Polish characters in To header | Use RFC 2047 encoding: `formataddr((str(Header(to_name, 'utf-8')), to_email))` |
| Google blocks after ~50 automations | Re-login Firefox between batches, limit to 40 per session |
| Firefox profile triggers re-auth | Expected behavior, Google security feature |
| `MoveTargetOutOfBounds` on compose | Run `caffeinate -d` and `maximize_window()` before operations |

## Campaign Strategy (Best Practices)

| Parameter | Value |
|-----------|-------|
| Daily email budget | 40–50 (safe/max) |
| New emails per day | 25–30 |
| Follow-ups per day | 15–20 |
| Optimal send time | 8:30 CET (new), 13:00 CET (follow-up) |
| Best days | Tuesday, Wednesday, Thursday |
| Delay between sends | 90–120 seconds |
| Follow-up wait time | 5 days after initial |
| Max follow-ups per venue | 2 (3 total touches) |
| Expected campaign duration | 11–12 business days |
| Gmail daily limit | 500 emails/day (free accounts) |

**Key Rules:**
- **NEVER auto-send** without user confirmation (no `echo "yes" |`)
- **Always use `--draft` mode** — user reviews in Gmail before sending
- Don't send all follow-ups in one day — sudden spike triggers blocks
- Vary follow-up angle (video, specific date, press kit, personal touch)
- Follow-ups count toward daily limit but are softer on reputation when threaded

## Data Flow

```
Facebook events (JSON)
    ↓
Classification (VENUE/ORG/MUSICIAN/NOISE)
    ↓
DuckDuckGo search + contact scraping
    ↓
Email prioritization (score 100→40)
    ↓
contacts_final.csv (426 venues, best email each)
    ↓
campaign.py (personalization)
    ↓
Gmail drafts (IMAP) or Gmail Sent (SMTP)
    ↓
schedule_drafts.py (Selenium scheduling)
    ↓
decisions_log.csv (audit trail)
```

## Tech Stack

- **Python 3.11** — main scripting language
- **Selenium** — Firefox automation for Gmail UI
- **geckodriver 0.30.0** — WebDriver for Firefox (High Sierra compatible)
- **Gmail SMTP** — email sending (smtp.gmail.com:587 STARTTLS)
- **Gmail IMAP** — draft creation
- **DuckDuckGo** — contact research
- **BeautifulSoup** — HTML parsing

## License

MIT

## Contact

For questions about this campaign system or the Kolot the Voices band:
- **Project Owner:** Dima Gorelik (dimagorelick@gmail.com)
- **Booking Agent:** Noa
- **Website:** [Kolot the Voices](https://kolotthevoices.com)
