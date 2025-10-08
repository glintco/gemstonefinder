[README.md](https://github.com/user-attachments/files/22758010/README.md)
# Gemstone Finder

A lightweight, single-file website that lists gemstones with Mohs hardness, optical/physical properties, and common treatments. Data is loaded from a **Google Sheet (CSV)** so non-technical editors can update content.

Live demo: Your GitHub Pages URL will look like:
`https://YOUR-USERNAME.github.io/REPO-NAME/`

---

## 1) Connect a Google Sheet (CSV)

**Sheet columns (case-insensitive):**
```
name, family, color, colors, hardness, ri, sg, luster, cleavage, toughness,
treatment_common, properties, price_tier, notes, sources, use
```

- Use **semicolons** for multi-values: `colors = Blue;Green;Pink`
- `sources` format: `Label|https://link; Label2|https://link2`
- Optional `use` overrides the auto “Recommended use” tag (otherwise computed from hardness/toughness/cleavage)

**Steps:**
1. Import `gemstones_template.csv` into Google Sheets (`File → Import → Upload`).
2. Share the sheet: **Anyone with the link: Viewer**.
3. **File → Share → Publish to web → Link → CSV → Publish** → copy the URL.
4. Open the site and click **Connect Google Sheet** (top-right), paste the CSV URL.

> If the CSV is unreachable, the app falls back to built-in demo data.

---

## 2) Edit data

Add or update rows in the sheet and republish. The site fetches the CSV on each load. Keep numeric fields numeric (e.g., `hardness=7.5`, `sg=2.72`). Ranges like `ri=1.762–1.770` are OK.

### Recommended values
- **hardness:** 1–10 (Mohs)
- **toughness:** `Poor`, `Fair`, `Good`, `Excellent`
- **cleavage:** `None`, `Indistinct`, `Good`, `Perfect (...)`

---

## 3) (Optional) Bake your Sheet URL into the site

So visitors don’t need to click **Connect Google Sheet**, set a default in `index.html`:

Search for:
```js
let SHEET_CSV_URL = localStorage.getItem('gem_csv_url') || '';
```
Replace with:
```js
let SHEET_CSV_URL = localStorage.getItem('gem_csv_url') || 'https://docs.google.com/spreadsheets/d/YOUR_SHEET_ID/pub?output=csv';
```

Then (optional) hide the button:
```html
<button class="btn" id="connectSheet" style="display:none">Connect Google Sheet</button>
```

Commit and push. From now on, the site auto-loads your sheet.

---

## 4) Customize

- **Title & description:** Edit `<title>` and add `<meta name="description" ...>` in `<head>`.
- **Branding:** Adjust colors in the `:root { ... }` CSS block.
- **Custom domain:** Repo **Settings → Pages → Custom domain** and follow the DNS instructions.
- **Analytics:** Add a script (e.g., Plausible, Cloudflare Web Analytics) in `<head>`.

---

## 5) Troubleshooting

- **Page 404:** Check **Settings → Pages** is `Deploy from a branch → main → /(root)`.  
- **CSV not loading:** Ensure you’re using a **Publish to web** CSV link (not an /edit link), and the sheet is public. Paste it in a tab—if it downloads/prints raw CSV, it’s valid.  
- **Filters empty:** Confirm column names and data types; refresh the page.  
- **Tanzanite family:** Use `Zoisite`.

---

## 6) Contributing

- Edit `index.html` for UI tweaks or new fields.
- For images, add a column `image_url` to the sheet and render it in the card (requires small code change).

---

## License

MIT
