# GitHub Project Explorer

An interactive dashboard to discover trending GitHub repositories, filter and sort them, see analytics charts, and bookmark repos with personal notes.

**Stack:** React 18, GitHub REST API, Chart.js, Tailwind CSS (all loaded from CDNs, so there is nothing to install).

## How to run
1. Open `index.html` in Chrome or Edge (double-click, or use VS Code "Live Server").
2. To host it free: push the folder to GitHub, then Settings → Pages → deploy from `main`.

> It must be opened in a normal browser with internet. Search API limit: about 10 requests per minute without a token, 30 with one.

## Requirement checklist (from the internship brief)
| Requirement | Where it is |
|---|---|
| Fetch data with GitHub REST API | `gh()` function calls `/search/repositories` |
| Sort by stars, language, update date | Sort dropdown (stars / forks / updated) and Language dropdown |
| Search and tag-based filters | Search box, topic input, and clickable topic chips on cards |
| Charts of contributions, issues, etc. | `ChartBox`: language mix, top stars, open issues, plus a per-repo top-10 contributors chart (`Details` popup, `/contributors` endpoint) |
| Bookmarking and note-taking | ★ button + notes textarea, saved in `localStorage` |

## How it works (the flow to explain in interviews)
1. **State:** `useState` holds every filter (query, language, topic, sort, period, page), the results, loading/error, and bookmarks.
2. **Debounce:** `useDebounce` waits 500 ms after typing stops, so we don't call the API on every keystroke (saves rate limit).
3. **Query building:** `useMemo` builds the GitHub search string, e.g. `react language:JavaScript topic:ui created:>2026-10-23`. "Trending" means new repos sorted by stars, because GitHub has no official trending API.
4. **Fetching:** a `useEffect` runs whenever the URL changes. A `live` flag in its cleanup ignores outdated responses (avoids race conditions).
5. **Caching:** a `Map` stores responses by URL, so going back to a page costs zero API calls.
6. **Rate limits and errors:** the `x-ratelimit-remaining` header is shown on screen, and 403/429/422 responses become friendly messages.
7. **Charts:** data is derived from the repos on screen with `useMemo`. `ChartBox` creates a Chart.js chart in `useEffect` and destroys it in the cleanup.
8. **Bookmarks:** stored as `{ full_name: { repo, note } }` in `localStorage`, so they survive a refresh. Notes are controlled components.
9. **Dark mode:** toggles Tailwind's `dark` class on `<html>` and is remembered.

## Interview questions this project answers (from the Top 50 list)
- **#19 Debouncing:** the search/topic/token inputs.
- **#17, #18 Async and promises:** `gh()` uses `async/await`; the effect uses `.then().catch().finally()`.
- **#21, #24 Hooks, props and state:** `useState`, `useEffect`, `useMemo`, `useRef`; props passed to `Card` and `ChartBox`.
- **#22 Controlled components:** every input is bound to state; notes textarea too.
- **#25 Lifting state up:** bookmarks live in `App`, and `Card` only receives callbacks.
- **#26 Keys:** `key={r.id}` on cards.
- **#27 useEffect cleanup:** chart destroy and the `live` flag.
- **#37, #43, #45 REST, HTTP methods, status codes:** GET requests, handling 403/422.
- **#47 CORS:** GitHub's API allows browser calls, so no proxy is needed.

Be ready to answer: *"Why a token field?"* (higher rate limit; for production, keep the token on a backend, never in frontend code).

## Easy upgrades if you have time
- **Backend:** save bookmarks/notes in Node + Express + MongoDB so they sync across devices (turns this into a full-stack project).
- **Contributors chart:** call `/repos/{owner}/{repo}/contributors` in a details modal.
- **Commit activity chart:** `/repos/{owner}/{repo}/stats/commit_activity`.

## Draft text for the 2-page report
**Introduction:** Developers need a quick way to find relevant open-source projects. This project is a web dashboard that explores GitHub repositories with filters and analytics.

**Abstract:** The app uses the GitHub REST API to fetch repositories, supports search, language and topic filters, sorting by stars, forks and update date, visualizes language, stars and issues data using Chart.js, and lets users bookmark repositories with notes stored locally.

**Tools Used:** React, GitHub REST API, Chart.js, Tailwind CSS, localStorage, GitHub Pages.

**Steps:** (1) Studied the Search API and built the query builder. (2) Created the React state and fetch logic with debounce and caching. (3) Added sorting, search and topic filters. (4) Built the chart components. (5) Added bookmarks and notes. (6) Handled errors and rate limits, added dark mode, tested, and deployed.

**Conclusion:** The project delivers a responsive, interactive explorer and taught me API integration, state management, data visualization and performance optimization.
