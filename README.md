# 🔭 GitHub Project Explorer

An interactive dashboard to discover popular GitHub repositories, filter and sort them, view analytics charts, and bookmark repos with personal notes. Built as part of my Web Development internship project at Elevate Labs.

🔗 **Live demo:** https://pasunoorimanaswini-beep.github.io/github-project-explorer/

## Features
- Search repositories using the GitHub REST API
- Filter by language, topic tag, minimum stars and creation period
- Sort by stars, forks or last updated
- Charts for language distribution, top repos by stars, open issues, and top contributors of any repo
- Bookmark repositories and add personal notes (saved in the browser)
- Dark mode, pagination, and rate-limit handling

## Tech Stack
React 18 · GitHub REST API · Chart.js · Tailwind CSS · JavaScript (ES6+)

## Run Locally
1. Clone this repository
2. Open `index.html` in a browser (or use VS Code Live Server)

> Without a GitHub token, the search API allows about 10 requests per minute. You can paste an optional token in the app for a higher limit.

## Highlights
- Debounced search to reduce unnecessary API calls
- In-memory caching of API responses
- Friendly error messages when the GitHub rate limit is reached

## Author
**Pasunoori Manaswini**
B.Tech CSE, Matrusri Engineering College
GitHub: [@pasunoorimanaswini-beep](https://github.com/pasunoorimanaswini-beep)
