# SE Calendar Studio

A single-file, browser-only tool that generates realistic, multi-week calendars for Solutions Engineering / Technical Sales teams and exports them as an RFC 5545 `.ics` file you can import into Outlook, Google Calendar, or Apple Calendar.

Use it to populate demo tenants, seed test calendars, exercise calendar integrations, or load-test scheduling tooling with believable data, without touching anyone's real schedule.

> **All generated data is synthetic.** People, email addresses, and Microsoft Teams join links are fabricated. See [Responsible use](#responsible-use) before importing into a calendar connected to a real mail system.

## Features

**Batch generation**
- Generate 1–2,000 work meetings across a date range (presets: 2 weeks, 1 month, quarter, or a custom range picker).
- Meeting durations sampled from the options you enable (15, 30, 45, 60, 90, 120 min).
- Monday–Friday only, inside an 08:00–18:00 local-time window.
- Min / max meetings per day and an optional fixed daily lunch block (12:00–12:45).
- Collision check: no two events on the generated calendar overlap.

**Activity profiles with weighted selection**
- Default work profiles: `[DISC]` Discovery, `[POC]` POC Support, `[RFP]` RFP Deep Dive, `[ENABLE]` Enablement, `[DEMO]` Product Demo, `[EBR]` Executive Briefing, `[1:1]` SE Sync, `[CLOSE]` Closeout, `[KICK]` Kickoff, `[MKTG]` Marketing Sync, `[HLTH]` HealthCheck, `[EVAL]` Eval Session.
- Default personal profiles: `[LUNCH]`, `[DOC]`, `[ERRAND]`, `[TRAVEL]` (full day), `[PTO]` (full day).
- Each profile has a 1–100 frequency weight. **Reroll Weights** re-randomizes within ranges (work 40–100, personal 1–39, PTO 1–10).
- Add, edit, or delete profiles.

**Roster, domains, and the primary user**
- Internal SEs / AEs use a configurable company domain; external guests use a configurable list of client domains.
- Email addresses are auto-generated in varied formats (`first.last`, `f.last`, `first_last`, …).
- A **primary user** is placed on every generated meeting, with sliders for organizer-vs-attendee ratio, accepted-vs-tentative ratio, and required-vs-optional ratio.
- Other attendees get randomized responses (≈70% accepted, 15% tentative, 10% no response, 5% declined) and per-person required/optional weighting.

**Export and persistence**
- `.ics` export with `ORGANIZER`, `ATTENDEE` (`ROLE`, `PARTSTAT`), `STATUS`, and `X-MICROSOFT-CDO-BUSYSTATUS` set from the primary user's response.
- Text escaping and 75-octet line folding per RFC 5545.
- Roster, domains, activity profiles, and slider settings persist in the browser's `localStorage`. Nothing is sent to a server.

## Quick start

No build step and no server. Open the file in a modern browser (Chrome, Edge, Firefox, Safari).

```bash
git clone https://github.com/egarlepp/calendar_studio.git
```

Then open `calendar_studio/index.html`.

An internet connection is required on first load: Tailwind CSS and the Inter font are fetched from public CDNs.

### Hosting on GitHub Pages

1. In the repository, go to **Settings → Pages**.
2. Under **Build and deployment**, choose **Deploy from a branch**, branch `main`, folder `/ (root)`.
3. The app is served from `index.html` at the URL GitHub shows.

## Usage

1. **Domains** – click the domain badge in the header to set the company domain and the client guest domains.
2. **Roster** – in **Team Roster & Guests**, add internal SEs/AEs or external guests (or click **+ Random Client Guest**).
3. **Activity profiles** – in **Activity Profiles**, adjust frequency weights or add custom profiles.
4. **Generate** – in **Batch Generator**, pick the date range, target count, min/max per day, durations, primary user, and attendees, then click **Generate Calendar Batch**.
5. **Review and export** – in **Schedule Preview**, filter or remove events, then click **Export .ICS File for Outlook**.

### Importing into Outlook (desktop)

**File → Open & Export → Import/Export → Import an iCalendar (.ics) or vCalendar file**, then choose **Import** (not **Open as New**) to merge events into the target calendar.

> The target-count field is an upper bound. Generation stops early when every business day has reached its randomly chosen daily cap (between your min and max), so short ranges with a low max/day produce fewer meetings than requested.

## Sample output

```text
BEGIN:VCALENDAR
VERSION:2.0
PRODID:-//SE Calendar Studio//Batch Generator v3.6//EN
CALSCALE:GREGORIAN
METHOD:PUBLISH
BEGIN:VEVENT
UID:evt_k9x2p1a8z@securwrix.com
DTSTAMP:20260806T143000Z
DTSTART:20260901T130000Z
DTEND:20260901T140000Z
SUMMARY:[DISC] Discovery Session - Elena Rostova
DESCRIPTION:Activity Type: [DISC]\nSubject: Discovery Session - Elena Rosto
 va\n...
ORGANIZER;CN=Alex Rivera:MAILTO:alex.rivera@securwrix.com
ATTENDEE;CN=Alex Rivera;ROLE=REQ-PARTICIPANT;PARTSTAT=ACCEPTED;RSVP=TRUE:MA
 ILTO:alex.rivera@securwrix.com
ATTENDEE;CN=Elena Rostova;ROLE=REQ-PARTICIPANT;PARTSTAT=TENTATIVE;RSVP=TRUE
 :MAILTO:elena.rostova@acmecorp.example
STATUS:CONFIRMED
X-MICROSOFT-CDO-BUSYSTATUS:BUSY
END:VEVENT
END:VCALENDAR
```

Times are written in UTC (`Z`), converted from the browser's local time zone at generation time.

## Responsible use

- Default client guest domains, and those created by **+ Random Client Domain**, use the reserved `.example` top-level domain ([RFC 2606](https://www.rfc-editor.org/rfc/rfc2606)), so they cannot reach real inboxes.
- The company domain and any guest domains you enter yourself are used as-is. If a domain is real, generated addresses may belong to real people. Prefer domains you own or reserved test domains (`example.com`, `*.example`, `*.test`) when the calendar is connected to a live mail system.
- Settings are saved in `localStorage`, so a browser that used an earlier version keeps its previously saved domains until you change them in the domain settings.
- Importing an `.ics` with `METHOD:PUBLISH` adds events locally and does not send invitations, but forwarding, editing, or re-sending those events from a mail client can email the listed attendees.
- The Teams links are random strings in Teams URL format; they do not correspond to real meetings.
- This project is not affiliated with or endorsed by Microsoft. Outlook and Microsoft Teams are trademarks of Microsoft Corporation.

## Tech stack

- Single static HTML file, vanilla ES2020+ JavaScript, no build tooling.
- [Tailwind CSS](https://tailwindcss.com) via the Play CDN, [Inter](https://fonts.google.com/specimen/Inter) via Google Fonts.
- Browser `localStorage` for persistence.

## Contributing

Issues and pull requests are welcome.

1. Fork the repository and create a branch (`git checkout -b feature/my-change`).
2. Keep the app a single, dependency-free `index.html` unless the change discusses otherwise in an issue first.
3. Test in at least one Chromium-based browser and one non-Chromium browser, and import a generated `.ics` into a calendar client.
4. Open a pull request describing the change and how you tested it.

To report a security issue, see [SECURITY.md](SECURITY.md).

## License

[MIT](LICENSE)
