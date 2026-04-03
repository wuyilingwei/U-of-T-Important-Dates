# U of T Important Dates — Calendar Feed

> **⚠ NOT AN OFFICIAL UNIVERSITY PRODUCT.**  
> This is an independent student convenience tool, not affiliated with or endorsed by the University of Toronto or UTM.  
> Always verify important dates at the **[official UTM Registrar page](https://www.utm.utoronto.ca/registrar/dates)**.

Automatically-updated `.ics` calendar file for the **University of Toronto Mississauga** Registrar's important academic dates.  
The calendar is rebuilt once per day by GitHub Actions and served as a static file via GitHub Pages.

---

## Subscribe — stays current automatically

Add the webcal feed to your calendar app. When the UTM Registrar publishes new dates, your calendar will pick them up on its next sync.

| Calendar App | Action |
|---|---|
| Apple Calendar / iOS | Click: **[webcal://wuyilingwei.github.io/U-of-T-Important-Dates/utm.ics](webcal://wuyilingwei.github.io/U-of-T-Important-Dates/utm.ics)** |
| Google Calendar | [Click to add »](https://calendar.google.com/calendar/r?cid=webcal%3A%2F%2Fwuyilingwei.github.io%2FU-of-T-Important-Dates%2Futm.ics) |
| Outlook (desktop) | File → Open & Export → Import/Export → Import an iCalendar file → paste the https:// URL |
| Thunderbird | New Calendar → On the Network → paste the webcal:// URL |

**webcal URL:**
```
webcal://wuyilingwei.github.io/U-of-T-Important-Dates/utm.ics
```

**https URL (for apps that prefer https):**
```
https://wuyilingwei.github.io/U-of-T-Important-Dates/utm.ics
```

---

## Download — static one-time import

[⬇ Download utm.ics](https://wuyilingwei.github.io/U-of-T-Important-Dates/utm.ics)

Import this into any calendar app. The file will **not** update automatically after download.

---

## Project page

**[wuyilingwei.github.io/U-of-T-Important-Dates](https://wuyilingwei.github.io/U-of-T-Important-Dates)**

---

## Technical details

| Item | Value |
|---|---|
| Data source | <https://www.utm.utoronto.ca/registrar/dates> |
| Update schedule | Daily at 08:00 UTC (GitHub Actions cron) |
| Rendering method | Playwright headless Chromium — dates are loaded by an Elfsight JS widget and are absent from raw HTML |
| Event type | All-day `VEVENT` entries (RFC 5545) |
| User-Agent | `U-of-T-Calendar-Bot/1.0 (Contact: sy.lei@mail.utoronto.ca; Student Project)` |
| Output | `docs/utm.ics` — served by GitHub Pages |
| Supported campuses | UTM (more planned) |

### Why Playwright?

The UTM registrar dates page embeds an **Elfsight** third-party calendar widget that renders content entirely client-side via JavaScript. A plain HTTP request returns only the page shell without any date entries. Playwright renders the full page, waits for the widget to hydrate, then extracts the text.

---

## Running locally

```bash
# Install Python dependencies
pip install -r scripts/requirements.txt

# Install the headless browser
playwright install chromium --with-deps

# Generate docs/utm.ics
python scripts/scrape_utm.py

# Optional flags
python scripts/scrape_utm.py --verbose               # DEBUG logging
python scripts/scrape_utm.py --debug rendered.html   # save rendered HTML
python scripts/scrape_utm.py --output /tmp/test.ics  # custom output path
```

---

## Disclaimer

This project is **not** affiliated with, sponsored by, or endorsed by the University of Toronto, the University of Toronto Mississauga, or any of their staff or departments.

Data is sourced from the publicly accessible UTM Registrar website for personal convenience. Use at your own risk. The maintainer accepts no responsibility for any errors or omissions in the calendar data.
