# PSS Pickleball Smash Out Series website

## Included
- `index.html` – responsive public scoreboard + organizer dashboard
- `pss-logo.png` – your supplied PSS logo
- `firestore.rules` – public read, authenticated-organizer write rules

## Before publishing
This is a Firebase-backed live website. GitHub Pages alone cannot sync scores across phones; Firebase Firestore provides the shared live database.

### 1. Create Firebase project
1. Go to https://console.firebase.google.com/ and create a project.
2. Add a Web App and copy its Firebase config.
3. In `index.html`, replace the six `PASTE_...` values in `firebaseConfig`.
4. In Firebase Authentication → Sign-in method, enable **Email/Password**.
5. In Authentication → Users, create one organizer account (use an email and a strong password known only to the organizer).
6. In Firestore Database, create a database.
7. Open Firestore → Rules and paste `firestore.rules`, then Publish.

### 2. Publish with GitHub Pages
Upload `index.html`, `pss-logo.png`, and `firestore.rules` to the same folder in your GitHub repository. Enable GitHub Pages from Settings → Pages. Open the published site URL.

## Tournament logic
- Six teams, 15 single round-robin fixtures, five matches per team.
- Fixtures are all visible from the beginning; organizer marks them Playing / Completed.
- A team already in a Playing match cannot be started in another match.
- Round-robin generator ensures no repeat opponents.
- Win +2 / loss −2 league points; standings show wins, losses, point difference and points scored.
- Top two qualify after all 15 league matches; organizer creates one Grand Final.
- Public pages are read-only; score changes stream live from Firestore without refreshing.

## Important security note
The organizer uses Firebase Authentication, not a hard-coded PIN in the HTML. A PIN checked only in browser JavaScript can be discovered by visitors and is not secure. Do not put your organizer password or Firebase service-account keys in this repository. Only create the organizer account; do not create public write access.

## PSS match scoring
The form validates a completed game as at least 11 points with a two-point winning margin. If your event uses a different scoring rule, adjust the validation in the `data-save` handler in `index.html`.
