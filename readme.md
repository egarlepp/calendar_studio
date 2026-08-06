# **📅 SE Calendar Studio & Batch ICS Generator**

> **An enterprise-grade, zero-dependency web application for Systems Engineering, Technical Sales, and Solutions Architecture teams to simulate, batch-schedule, and export realistic multi-month team calendar events to Microsoft Outlook.**

## **🌟 Key Features**

### **1\. ⚙️ High-Volume Batch Generator Engine**

* **Scalable Batch Volumes**: Generate anywhere from 5 to **2,000+ meetings** in a single run.  
* **Flexible Date Horizons**: Quickly apply date range presets (2 Weeks, 1 Month, Quarter/3 Months) or define custom start/end dates.  
* **Randomized Duration Selection**: Randomly sample meeting durations across standard intervals (15m, 30m, 45m, 60m, 90m, 120m).

### **2\. 🛡️ Smart Workday Constraints & Gap Logic**

* **Monday–Friday Strictly**: Automatic weekend skipping.  
* **10-Hour Workday Window**: All meetings strictly schedule between **08:00 AM and 06:00 PM**.  
* **Anti-Stacking Limits**: Define a maximum meeting cap per day to prevent schedule congestion.  
* **Anti-Overlap Collision Engine**: Checks existing day schedules before placing new events to guarantee zero double-booking.

### **3\. 🎯 Multi-Activity Profiles & Weighted Probability**

* **Work Activity Profiles**: Pre-loaded with standard SE lifecycle sessions:  
  * \[RFP\] RFP Alignment  
  * \[POC\] Technical POC Support  
  * \[DISC\] Discovery Session  
  * \[ENABLE\] Technical Enablement  
  * \[TCC\] Technical Architecture Review  
  * \[DEMO\] Product Demo  
  * \[EBR\] Executive Briefing  
  * \[HEALTH\] HealthCheck  
  * \[CLOSE\] Account Closeout  
  * \[KICKOFF\] Project Kickoff  
* **Weighted Selection Engine (1–100 Frequency Sliders)**: Set frequency probability weights for each meeting type. Work meetings default to high frequency (40–100), personal activities to lower frequency (1–39), and PTO to rare frequency (1–10). Includes a **Reroll Weights** action.  
* **Full-Day Event Locking**: Full-day events like \[PTO\] (PTO/Vacation) and \[TRAVEL\] (Business Travel) lock out the full 10-hour workday to prevent work meeting overlap.

### **4\. 👥 Team Roster & Guest Domain Management**

* **Domain Guardrails**:  
  * **Internal Team**: SEs and Sales Account Executives (AEs) strictly enforce the corporate domain (Default: @securwrix.com).  
  * **External Guests**: External clients are assigned to randomized or selected partner domains (e.g. @testing.com, @acemcorp.com, @apex-corp.com).  
* **Rotating Meeting Organizers**: Organizers are dynamically rotated among internal SEs/AEs.  
* **Automated Email Formatter**: Generates realistic email addresses using varied patterns (first.last, f.last, first\_last, last, etc.) with a single-click "Randomize Format" generator.

### **5\. ✉️ Rich Event Descriptions & Teams Integration**

* **Auto-Generated Meeting Agendas**: Automatically includes structured agendas (Scope & Objective Overview, Technical Alignment, Action Items).  
* **Simulated Microsoft Teams Links**: Generates standard Teams join URLs (https://teams.microsoft.com/l/meetup-join/...).  
* **Participant Response Tracking (PARTSTAT)**: Simulates realistic attendee responses (**Accepted** \~70%, **Tentative** \~15%, **Pending** \~10%, **Declined** \~5%) rendered with visual badges in the preview table and encoded into iCalendar outputs.

### **6\. 📤 Outlook RFC 5545 .ICS Export & Local Persistence**

* **Standard-Compliant .ICS Export**: Instant export compatible with Microsoft Outlook Desktop, Outlook Web, Office 365, Apple Calendar, and Google Calendar.  
* **Automatic State Persistence**: Configurations, custom team members, domain updates, and activity weights automatically persist in browser storage.

## **🚀 Quick Start**

Because this application is built as a single, self-contained file with embedded dependencies, **no server, build tools, or Node.js runtime are required**.

### **Option A: Direct Local Execution**

1. Clone or download this repository:  
   git clone https://github.com/your-username/se-calendar-studio.git  
   cd se-calendar-studio

2. Open index.html in any modern web browser (Chrome, Edge, Firefox, Safari).

### **Option B: Hosting via GitHub Pages**

1. Push index.html to a GitHub repository.  
2. Navigate to **Settings \> Pages** in your GitHub repo.  
3. Select the main branch as the source.  
4. Access your live deployment link provided by GitHub Pages.

## **📖 Usage Guide**

┌─────────────────────────────────────────────────────────────────┐  
│                      SE CALENDAR STUDIO WORKFLOW                │  
└─────────────────────────────────────────────────────────────────┘  
         │  
         ▼  
 1\. Configure Domains & Roster ─────► Set primary corporate domain & guest list  
         │  
         ▼  
 2\. Set Activity Weights      ─────► Adjust frequency sliders (1-100) or reroll  
         │  
         ▼  
 3\. Define Date Range & Rules  ─────► Select start/end dates & daily max limits  
         │  
         ▼  
 4\. Run Batch Generator        ─────► Auto-builds conflict-free calendar  
         │  
         ▼  
 5\. Export .ICS to Outlook     ─────► Import batch directly into target calendar

### **Step 1: Configure Environment & Domain**

* Click the **Domain Badge** in the top header (@securwrix.com).  
* Set your primary company domain for internal SEs and Sales Reps.  
* Add or customize client guest domains (e.g. clientcorp.com). Click \+ Random Client Domain to quickly generate samples.

### **Step 2: Customize Roster & Attendees**

* Navigate to the **Team Roster & Guests** tab.  
* Add internal SEs/AEs or client guests.  
* External client guests provide a dropdown selector of your saved client domains and auto-generate randomized email formats as you type the member's name.

### **Step 3: Configure Activity Profiles & Frequency Weights**

* Navigate to the **Activity Profiles** tab.  
* Adjust the frequency weight slider (1–100) for any session type to increase or decrease how often it gets selected.  
* Click **Reroll Weights** to re-randomize activity probabilities within compliant ranges (Work: 40-100, Personal: 1-39, PTO: 1-10).

### **Step 4: Run Schedule Generation**

* Navigate to the **Batch Generator** tab.  
* Pick your date range (e.g. 3 Months / Quarter) and set your **Target Work Meetings** count (up to 2,000).  
* Set your **Max Meetings / Day** cap and toggle **Auto Daily Lunch Break** (\[LUNCH\] 12:00 PM \- 12:45 PM).  
* Click **Generate Calendar Batch**.

### **Step 5: Preview & Export to Outlook**

* Switch to the **Schedule Preview** tab to review generated meetings, total hours, unique attendees, and response statuses.  
* Filter by category (Work vs. Personal) or search by keyword/attendee name.  
* Click **Export .ICS File for Outlook** to save the .ics file.  
* Open Outlook, go to **File \> Open & Export \> Import/Export \> Import an iCalendar (.ics) file**, and select your target shared calendar.

## **📄 iCalendar (.ICS) Standard Compliance**

The output generated by SE Calendar Studio adheres strictly to the **RFC 5545 iCalendar specification**:

BEGIN:VCALENDAR  
VERSION:2.0  
PRODID:-//SE Calendar Studio//Batch Generator v3.0//EN  
CALSCALE:GREGORIAN  
METHOD:PUBLISH  
BEGIN:VEVENT  
UID:evt\_k9x2p1a8z@securwrix.com  
DTSTAMP:20260806T143000Z  
DTSTART:20260901T130000Z  
DTEND:20260901T140000Z  
SUMMARY:\[DISC\] Discovery Session \- Elena Rostova  
DESCRIPTION:Activity Type: \[DISC\]\\nSubject: Discovery Session...\\n\\nMicrosoft Teams Meeting\\nJoin Link: https://teams.microsoft.com/...  
ORGANIZER;CN=Alex Rivera:MAILTO:alex.rivera@securwrix.com  
ATTENDEE;CN=Alex Rivera;PARTSTAT=ACCEPTED;RSVP=TRUE:MAILTO:alex.rivera@securwrix.com  
ATTENDEE;CN=Elena Rostova;PARTSTAT=ACCEPTED;RSVP=TRUE:MAILTO:elena.rostova@acemcorp.com  
STATUS:CONFIRMED  
END:VEVENT  
END:VCALENDAR

## **🛠️ Tech Stack & Dependencies**

* **UI Framework**: [Tailwind CSS v3](https://tailwindcss.com) (Loaded via CDN)  
* **Typography**: [Inter](https://fonts.google.com/specimen/Inter) via Google Fonts  
* **Icons**: Inline SVG System  
* **Runtime**: Pure Client-Side ES6+ JavaScript  
* **Storage**: Browser localStorage API

## **🤝 Contributing**

Contributions, feedback, and enhancement requests are welcome\!

1. Fork the Project.  
2. Create your Feature Branch (git checkout \-b feature/NewActivityType).  
3. Commit your Changes (git commit \-m 'Add new activity profile type').  
4. Push to the Branch (git push origin feature/NewActivityType).  
5. Open a Pull Request.

## **📝 License**

Distributed under the **MIT License**. See LICENSE for details.