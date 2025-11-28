📘 C.H.A.M.P. Website
Community Hub for Actualizing Mycological Passion

A modular, GitHub-Pages–hosted website for a decentralized mycology community

🌱 Quick Guide: How to Update the Site
(Most common tasks for new contributors)
✅ Add a New Event (Calendar + Frontpage auto-show)

Go to:
pages/dashboard/calendar/events/

Create a new .txt file, e.g.:
2025-12-01-winter-foray.txt

Use this format:

Title: Winter Foray
Date: 2025-12-01
Time: 10:00
Location: Crane Reservation
Description: A group foray focusing on cold-season fungi.

Commit and push — GitHub Actions will automatically update the calendar manifest.

Event will appear:

in the calendar page

in the frontpage event grid

in event detail pages (event.html?id=filename.txt)

No code changes needed.

✅ Add an Important Link

Go to:
pages/dashboard/links/items/

Create a new .txt file, e.g.:
discord.txt

Use this format:

Title: Community Discord
Url: https://discord.gg/yourlink
Description: Real-time coordination and chat.
Category: Community

Add the filename to:
pages/dashboard/links/index.json

{
"links": [
"champ-site.txt",
"discord.txt"
]
}

Commit & push — the link appears automatically on the frontpage.

✅ Update the Frontpage Suggestion Box Endpoint

Edit:

data/site-config.json

Example:

{
"suggestionBox": {
"endpoint": "https://formspree.io/f/your-form-id"
}
}

🏗️ Project Overview

This site is built to be:

Modular – each component is a “module” loaded dynamically

File-driven – events and links are text files (easy to edit, no coding)

GitHub Pages hosted – no server needed

Pure JS/HTML/CSS – no frameworks required

Automatic manifests – GitHub Actions keep event lists synchronized

Frontpage modules include:

Event Grid

News (placeholder)

Important Links

Suggestion Box

Dedicated pages:

Calendar (/calendar/)

Event details (event.html?id=<event-file>)

📂 Directory Structure (Important Parts)
champ-site/
│
├── index.html ← Frontpage
├── calendar/  
│ └── index.html ← Full calendar page
│
├── assets/
│ ├── css/style.css ← Global site styling
│ └── js/
│ ├── app.js ← Frontpage module loader
│ └── modules/
│ ├── calendar.js
│ ├── events-grid.js
│ ├── news-grid.js
│ ├── links-grid.js
│ ├── proton-feed.js
│ └── suggestion-box.js
│
├── data/
│ ├── modules.json ← Dictates which modules appear on frontpage
│ └── site-config.json ← Global config (API endpoints, etc.)
│
└── pages/
└── dashboard/
├── calendar/
│ ├── index.json ← Auto-built by GitHub Actions
│ └── events/ ← _.txt event files
│
└── links/
├── index.json ← Manually updated list of link txt files
└── items/ ← _.txt link files

💻 Developing Locally (VS Code)

1. Clone the repo
   git clone https://github.com/comm-hub-myco/champ-site.git
   cd champ-site

2. Open in VS Code
   code .

3. Install Live Server extension

In VS Code → Extensions → search: Live Server → Install.

4. Run the site

Right-click index.html → Open with Live Server.

Your site is now live at:
http://127.0.0.1:5500/

Changes auto-refresh on save.

🧠 How the Frontpage Works (Modules)

The frontpage is controlled by:

data/modules.json

{
"frontpage": [
"events-grid",
"news-grid",
"links-grid",
"suggestion-box"
]
}

app.js reads this and injects modules in the listed order.

Each module:

has a JS file in assets/js/modules/

creates and populates a section inside <main id="app">

To add a new frontpage module, you:

Create a module JS file

Add a block in app.js

Add its name to data/modules.json

🗓️ How the Calendar Works

Event files live in:
pages/dashboard/calendar/events/\*.txt

A GitHub Action auto-builds index.json whenever events change.

calendar.js loads both:

the manifest (index.json)

each event .txt file

The calendar page passes basePath: ".." so relative fetch paths work

Pills and dates link to the event detail page automatically

🔗 How the Links System Works

Link files live in pages/dashboard/links/items/\*.txt

You manually add filenames to pages/dashboard/links/index.json

links-grid.js reads these text files and renders link cards

📮 Suggestion Box

Anonymous submission form

Backend endpoint configured in data/site-config.json

Uses Formspree or any compatible POST endpoint

To change the endpoint:

{
"suggestionBox": {
"endpoint": "https://formspree.io/f/your-id"
}
}

🛠️ Adding a New Page

Create a folder (e.g., projects/)

Add index.html

Use a consistent header/footer from other pages

Add your scripts at the bottom:

<script defer src="https://cdn.jsdelivr.net/npm/luxon@3/build/global/luxon.min.js"></script>
<script defer src="../assets/js/app.js"></script>

Link to it from the nav using absolute GitHub Pages paths:

<nav class="site-nav">
  <a href="/champ-site/">Frontpage</a>
  <a href="/champ-site/calendar/">Calendar</a>
  <a href="/champ-site/projects/">Projects</a>
</nav>

🔧 GitHub Actions

One GitHub Action updates the event manifest automatically:

.github/workflows/build-manifests.yml

It runs whenever files in the events folder change and rebuilds:

pages/dashboard/calendar/index.json

You normally don’t need to touch this file.

🧩 Support & Contribution

This repo is designed to be edited by:

anyone familiar with GitHub

beginners who only need to edit .txt files

If contributing:

Keep formatting consistent

Use descriptive commit messages

Test in Live Server before pushing

🍄 Welcome to C.H.A.M.P.

The website grows like a mycelial network — each simple piece adds strength, structure, and opportunity for exploration.

If you have ideas, propose them in:
➡️ The Suggestion Box
➡️ GitHub Issues
