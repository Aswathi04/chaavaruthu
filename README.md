<p align="center">
  <img src="./img.png" alt="VolunteerFlow Banner" width="100%">
</p>

# VolunteerFlow 🍽️

## Basic Details

### Team Name: Anosha's Team

### Team Members
- Member 1: Anosha Roy - Viswajyothi College of Engineering and Technology
- Member 2: Aswathi Thummarukudy - Viswajyothi College of Engineering and Technology

### Hosted Project Link
[chaavaruthu-theta.vercel.app](https://chaavaruthu-theta.vercel.app)

### Project Description
VolunteerFlow is a capacity planning tool for nonprofit volunteers and their coordinators. Volunteers log their weekly tasks, tag each one as energizing, neutral, or draining, and watch their plate fill up in real time. Coordinators get a live dashboard showing who's carrying too much — before anyone burns out.

### The Problem Statement
Volunteers burn out silently. They say yes to more than they can carry, coordinators only find out when someone quits, and there's no lightweight tool that gives either side visibility into what's actually being given — and what it's costing.

### The Solution
VolunteerFlow reframes the check-in as a personal planning tool, not a wellness survey. Volunteers log named tasks with hours and emotional tags (energizing, neutral, draining), see their week visualised as a plate filling up, and get a reflection card after submitting. A weighted load formula — draining hours count 1.5x, energizing at 0.75x — means the plate reflects emotional cost, not just time. Coordinators see a live dashboard with mini plate visualisations per volunteer, colour-coded by capacity status, with one-click detail expansion.

---

## Technical Details

### Technologies/Components Used

**For Software:**
- Languages used: HTML, CSS, JavaScript
- Frameworks used: None — plain vanilla JS, no build tools
- Libraries used: D3.js (plate SVG visualisation), Firebase Realtime Database SDK
- Tools used: VS Code, Git, Vercel, Firebase Console

---

## Features

- **Task-based plate builder** — volunteers log real tasks by name, org, and hours rather than abstract hour estimates. The plate SVG updates live as tasks are added and tagged.
- **Emotional tagging** — each task is tagged energizing, neutral, or draining with a single tap. Tags drive the plate colour composition and the weighted load calculation.
- **Weighted capacity score** — draining hours × 1.5, neutral × 1.0, energizing × 0.75. The plate visually overflows when weighted load exceeds the volunteer's comfortable limit.
- **Weekly reflection card** — after submitting, volunteers see their plate composition as percentages, a plain-language insight about their week, and a comparison to last week's weighted load pulled from Firebase.
- **Plate portrait gallery** — the last 8 weeks shown as mini plates, clickable to review past task breakdowns. A visual record of what has been given over time.
- **Live coordinator dashboard** — real-time view of all volunteers with mini plate thumbnails, status badges (doing well / check in / needs attention), and an expandable detail panel with task list and capacity bar.
- **Autocomplete from history** — task names from previous weeks are saved to Firebase and surfaced as autocomplete suggestions, reducing friction on return visits.

---

## Implementation

### For Software:

#### Installation

No installation required. The project is plain HTML/CSS/JS loaded via CDN scripts. To run locally, simply open the files in a browser or serve with any static file server:

```bash
# Using Python
python -m http.server 8000

# Using Node
npx serve .
```

#### Run

```bash
# Open in browser
open index.html

# Or visit the hosted version
https://chaavaruthu-theta.vercel.app
```

---

## Project Documentation

### For Software:

#### Screenshots (Add at least 3)

![Screenshot1](docs/screenshot-landing.png)
*Landing page — volunteers and coordinators choose their view*

![Screenshot2](docs/screenshot-checkin.png)
*Volunteer check-in — task rows with live plate updating as tasks are tagged*

![Screenshot3](docs/screenshot-dashboard.png)
*Coordinator dashboard — mini plates per volunteer with status badges and expandable detail panel*

#### Diagrams

**System Architecture:**

```
Browser (HTML/CSS/JS)
        │
        ├── D3.js (via CDN) — SVG plate rendering
        ├── Firebase JS SDK (via CDN) — Realtime DB read/write
        │
Firebase Realtime Database
        │
        ├── /volunteers/{volunteerId}/weeks/{weekOf}/tasks[]
        ├── /volunteers/{volunteerId}/profile/capacityThreshold
        └── /volunteers/{volunteerId}/autocomplete/{taskName}
```

*No backend server. All logic runs client-side. Firebase handles persistence and real-time sync to the coordinator dashboard.*

**Application Workflow:**

```
Volunteer opens checkin.html
        │
        ├── Loads capacity threshold + autocomplete from Firebase
        ├── Loads existing tasks for current week if already submitted
        │
Volunteer adds tasks → tags each (🔥 😐 🪨) → plate updates live
        │
Volunteer clicks "Save my week"
        │
        ├── Writes tasks to Firebase: /volunteers/{id}/weeks/{weekOf}/tasks
        ├── Updates autocomplete index
        └── Shows reflection card (composition % + insight + last week comparison)
                │
                └── Gallery renders last 8 weeks from Firebase

Coordinator opens dashboard.html
        │
        ├── Firebase listener on /volunteers (real-time)
        ├── Computes weighted load per volunteer
        ├── Renders mini plate + status badge per card
        └── Click to expand → full plate + task list + capacity bar
```

---

## Firebase Data Structure

```json
{
  "volunteers": {
    "Priya": {
      "profile": {
        "capacityThreshold": 10
      },
      "autocomplete": {
        "Food bank sorting": true,
        "Volunteer emails": true
      },
      "weeks": {
        "2025-02-17": {
          "tasks": [
            {
              "id": "1708123456789",
              "name": "Food bank sorting",
              "org": "City Food Bank",
              "hours": 4,
              "tag": "draining"
            },
            {
              "id": "1708123456790",
              "name": "Volunteer onboarding",
              "org": "City Food Bank",
              "hours": 2,
              "tag": "energizing"
            }
          ]
        }
      }
    }
  }
}
```

---

## Weighted Load Formula

```
Weighted Load = (draining hours × 1.5) + (neutral hours × 1.0) + (energizing hours × 0.75)

Status thresholds (weighted load / capacity):
  ≤ 0.85  →  Doing well   (green)
  0.85–1.0 → Check in     (yellow)
  > 1.0   →  Needs attention (red)
```

The plate overflows its rim visually when weighted load exceeds capacity — no alert needed, the image says it.

---

## Project Demo

### Video
[Add demo video link here]

*Demo covers: volunteer adding tasks and watching the plate fill live → submitting and seeing the reflection card → coordinator dashboard showing real-time status → expanding a volunteer card for detail.*

### Additional Demos
[chaavaruthu-theta.vercel.app](https://chaavaruthu-theta.vercel.app)

---

## Team Contributions

- Anosha Roy: Product concept, UX design, volunteer check-in page (checkin.html), plate SVG visualisation, Firebase integration, reflection card and gallery logic
- Aswathi Thummarukudy: Coordinator dashboard (dashboard.html), real-time data sync, status logic, landing page (index.html), Vercel deployment

---

Made with ❤️ at TinkerHub
