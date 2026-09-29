# IPT Feedback

Static site (HTML/CSS/JS), cloned from the Canva version.

## 1. Add your images (required)
Export these from Canva and put them in `assets/`:
- `logo-menu.png` (menu page logo)
- `logo-year6.png` (Year 6 badge)
- `logo-year7.png` (Year 7 badge)

## 2. Connect submissions (required)
Canva's built-in data sheet doesn't exist outside Canva, so submissions need a new destination.

**Option A: Google Sheet (free)**
1. Create a Google Sheet. Row 1 headers: `year_level, email, week, worked_well, didnt_work, plan_changes, overall_rating, objectives_clarity, resources_effectiveness, student_engagement, other_notes, submitted_at`
2. Extensions > Apps Script, paste:
```js
function doPost(e) {
  const d = JSON.parse(e.postData.contents);
  const sh = SpreadsheetApp.getActiveSheet();
  const headers = sh.getRange(1, 1, 1, sh.getLastColumn()).getValues()[0];
  sh.appendRow(headers.map(h => d[h] ?? ""));
  return ContentService.createTextOutput("ok");
}
```
3. Deploy > New deployment > Web app > Execute as: Me, Who has access: Anyone. Copy the URL.
4. Paste the URL into `FORM_ENDPOINT` at the top of `script.js`.

**Option B: Formspree** – create a form and paste its endpoint URL instead.

## 3. Publish on GitHub Pages
1. Create a new GitHub repo and upload all files (keep `assets/`).
2. Settings > Pages > Deploy from branch > `main` / root > Save.
3. Your site appears at `https://<username>.github.io/<repo>/`.
