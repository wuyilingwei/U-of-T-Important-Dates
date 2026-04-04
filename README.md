# U of T Important Dates - Calendar Feed

> **NOT AN OFFICIAL UNIVERSITY PRODUCT.**
> This is an independent student convenience tool, not affiliated with or endorsed by the University of Toronto.
> Always verify important dates at the official registrar pages for your campus.

Automatically-updated .ics calendar files for three University of Toronto campuses.
The calendars are rebuilt once per day by GitHub Actions and served as static files via GitHub Pages.

---

## Campuses

| Campus | Webcal (auto-updates) | HTTPS URL | Official Source |
|---|---|---|---|
| **UTM** | webcal://wuyilingwei.github.io/U-of-T-Important-Dates/utm.ics | [utm.ics](https://wuyilingwei.github.io/U-of-T-Important-Dates/utm.ics) | [UTM Registrar](https://www.utm.utoronto.ca/registrar/dates) |
| **UTSC** | webcal://wuyilingwei.github.io/U-of-T-Important-Dates/utsc.ics | [utsc.ics](https://wuyilingwei.github.io/U-of-T-Important-Dates/utsc.ics) | [UTSC Registrar](https://www.utsc.utoronto.ca/registrar/academic-dates) |
| **ArtsCI** | webcal://wuyilingwei.github.io/U-of-T-Important-Dates/artsci.ics | [artsci.ics](https://wuyilingwei.github.io/U-of-T-Important-Dates/artsci.ics) | [ArtsCI Dates](https://www.artsci.utoronto.ca/current/dates-deadlines/academic-dates) |

---

## Subscribe - stays current automatically

Add the webcal feed to your calendar app. Your calendar will pick up new dates on its next sync.

| Calendar App | Steps |
|---|---|
| Apple Calendar / iOS | Click a webcal:// link above |
| Google Calendar | Use the Add to Calendar button on the [project page](https://wuyilingwei.github.io/U-of-T-Important-Dates/) |
| Outlook (desktop) | File > Open and Export > Import/Export > Import iCalendar > paste the webcal:// URL |
| Thunderbird | New Calendar > On the Network > paste the webcal:// URL |

---

## Download - static one-time import

Download any .ics file from the HTTPS URLs above and import into any calendar app.
The file will **not** update automatically after download.

---

## Project page

**[wuyilingwei.github.io/U-of-T-Important-Dates](https://wuyilingwei.github.io/U-of-T-Important-Dates)**

---

## Technical details

| Item | Value |
|---|---|
| Update schedule | Daily at 08:00 UTC (GitHub Actions cron) |
| Event type | All-day VEVENT entries (RFC 5545) |
| User-Agent | U-of-T-Calendar-Bot/1.0 (Contact: sy.lei@mail.utoronto.ca; Student Project) |

### Per-campus scraping method

| Campus | Method | Reason |
|---|---|---|
| UTM | Playwright headless Chromium | Dates loaded by an Elfsight JS widget - absent from raw HTML |
| UTSC | requests + BeautifulSoup (static) | Dates are in static HTML tables on registrar sub-pages |
| ArtsCI | Playwright + BeautifulSoup | Dates loaded via AJAX when Bootstrap accordion panels are clicked |

---

## Running locally

\\ash
pip install -r scripts/requirements.txt
playwright install chromium --with-deps
python scripts/scrape_utm.py
python scripts/scrape_utsc.py
python scripts/scrape_artsci.py
\
---

## Disclaimer

This project is **not** affiliated with, sponsored by, or endorsed by the University of Toronto or any of its campuses, staff, or departments.
