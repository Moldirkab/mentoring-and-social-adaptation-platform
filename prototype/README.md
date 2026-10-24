# Guiding Star (Путеводная звезда / Темірқазық) — static prototype

Interactive frontend prototype of the diploma project **"Development of a mentoring and social
adaptation platform for children from orphanages and graduates of boarding schools"**.

This folder is the ready-to-run build. It needs **no Node.js, no npm and no internet**:
just a web browser.

## What is in the folder

| File          | Purpose                                                                                                 |
| ------------- | ------------------------------------------------------------------------------------------------------- |
| `index.html`  | Entry page. Open this file.                                                                             |
| `styles.css`  | All styles ("Little Prince" palette: midnight blue, lavender, cream, gold, teal) and font declarations. |
| `app.js`      | The whole application: screens, RU/KK/EN translations, mock API with demo data, matching algorithm.     |
| `fonts/`      | Nunito and Cormorant Garamond font files (Latin + Cyrillic), so the page looks the same offline.        |
| `favicon.svg` | Browser tab icon.                                                                                       |

Keep the files together in one folder: `index.html` loads `styles.css`, `app.js` and `fonts/`
by relative paths.

## How to run

### Option 1. Open the file (simplest)

1. Unzip `prototype-static.zip` (if you downloaded the archive).
2. Double-click `index.html`, or drag it into a browser window.

Tested in Chromium (Chrome / Edge). Firefox and Safari also work with `file://` pages like this one.

### Option 2. Run a local web server (recommended for a demo or defence)

Some browsers or corporate policies limit pages opened from disk. A local server avoids that.
Open a terminal **in this folder** and run one of:

```bash
# Python 3 (Windows: use "py" instead of "python3")
python3 -m http.server 8000

# or Node.js, if installed
npx serve .
```

Then open **http://localhost:8000** in the browser. Stop the server with `Ctrl+C`.

### Option 3. Publish online

Upload the contents of this folder to any static hosting (GitHub Pages, Netlify, Vercel).
For GitHub Pages: put the files in the repository (for example in a `docs/` folder or a
`gh-pages` branch) and enable Pages in _Settings → Pages_. No server code is needed because
all pages use hash URLs (`index.html#/matching`).

## Demo accounts

Password for every account: **`prince2026`**

| Role        | E-mail            | What to try                                                                                                                                                                       |
| ----------- | ----------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Mentee      | `erlan@demo.kz`   | Home, profile, goals and lessons, meetings, chat with the mentor, "Report a problem"                                                                                              |
| Mentor      | `daniyar@demo.kz` | Chat, meetings (accept/propose), mentee goals, feedback after a meeting                                                                                                           |
| Coordinator | `aigerim@demo.kz` | Mentor applications (approve/reject), Matching (top-5 recommendations with score explanation and adjustable weights), create pairs, pair status and inactivity alerts, complaints |

Other seeded users (e.g. `elena@demo.kz`, `aliya@demo.kz`) use the same password.
A new mentor can also submit an application from the sign-in page ("Become a mentor").

## Suggested demo scenario (about 5 minutes)

1. Sign in as **aigerim@demo.kz** → _Mentor applications_ → approve an application.
2. _Matching_ → choose a mentee → see the top-5 mentors and the score breakdown
   (interests, city, time overlap, mentee preferences) → move a weight slider → create a pair.
3. Sign out (menu with your name) → sign in as **erlan@demo.kz** → _Goals_: add a goal,
   tick a lesson → _Chat_: send a message to the mentor.
4. Switch the language with the **RU / KZ / EN** button in the header. The choice is remembered.
5. Narrow the browser window (or open it on a phone) to show the responsive mobile layout.

## What is mocked (prototype limits)

The prototype is **frontend only**. Everything that a real server would do is simulated in the
browser:

- **Data storage.** All data lives in the browser's `localStorage` (keys `msap.demo-data`,
  `msap.session`). Each browser/computer has its own copy. Clear site data, or press the
  **Reset demo data** button, to start over.
- **Authentication.** Password check against the seeded demo users; no tokens, no real security.
- **AI matching.** Only the weighted rule-based score is computed (filters → weighted score → top 5).
  The embedding / LLM re-ranking step (FR-35 – FR-42) is shown as "needs the backend".
- **E-mail, SMS, push.** Not sent; notifications appear only inside the app.
- **File uploads** (documents for mentor verification) are not stored anywhere.
- **Video meetings.** A meeting stores a link; no video service is called.
- **Chat** is not real-time between devices: messages are saved locally.
- Network delay is simulated (a short pause on each call) so loading states are visible.

## How it maps to the microservice design

The screens never touch `localStorage` directly; they call one `MockApi` object. In the real
system each group of its methods becomes a REST call through the Traefik gateway to one of the
five FastAPI services (services talk to each other over gRPC):

| Service                      | MockApi methods used by the prototype                                                                                                                                                                                                                                                                                                                                               | Screens                                                         |
| ---------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------- |
| 1. Identity & Access         | `signIn`, `getUser`, `saveLanguagePreference`                                                                                                                                                                                                                                                                                                                                       | Sign-in, language switcher                                      |
| 2. Profile & Core Management | `updateProfile`, `submitApplication`, `listApplications`, `decideApplication`, `listMentors`, `listMenteesWithoutPair`                                                                                                                                                                                                                                                              | Profile, Become a mentor, Mentor applications, Mentor catalogue |
| 3. AI Matching               | `recommend`, `getWeights`, `saveWeights` (suggests only, never creates a pair)                                                                                                                                                                                                                                                                                                      | Matching → Recommendations                                      |
| 4. Mentoring & Progress      | `createPair`, `setPairStatus`, `listPairSummaries`, `getPairForUser`, `isInactive`, meetings (`listMeetings`, `proposeMeeting`, `respondToMeeting`, `cancelMeeting`, `recordMeetingOutcome`, `leaveFeedback`), goals (`listGoals`, `saveGoal`, `setGoalDone`, `deleteGoal`, `getTrackProgress`, `setLessonDone`), complaints (`reportProblem`, `listComplaints`, `updateComplaint`) | Home dashboards, Pairs, Meetings, Goals, Complaints             |
| 5. Communication & Signaling | `listMessages`, `sendMessage`, `setMessageHidden`, `listNotifications`, `unreadCount`, `markNotificationsRead`                                                                                                                                                                                                                                                                      | Chat, Notifications                                             |

Replacing the mock with a REST client that has the same method names is the only frontend
change needed to connect the real backend.

## About the code

`app.js` and `styles.css` are a compiled (minified) build of the prototype, written in
React + TypeScript. You do not need Node.js or any of the original source to run or show it:
the files in this folder are complete.
