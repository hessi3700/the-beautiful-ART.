# Get your site live on GitHub Pages

Follow these steps **on GitHub in your browser** (not on your computer).

---

## Step 1: Open Pages settings

1. Go to **https://github.com/hessi3700/the-beautiful-ART.**
2. Click **Settings** (top right of the repo).
3. In the left sidebar, click **Pages** (under "Code and automation").

---

## Step 2: Set "Deploy from a branch"

1. Under **"Build and deployment"**:
   - **Source**: choose **"Deploy from a branch"** (do **not** use "GitHub Actions").
2. Under **"Branch"**:
   - Branch: **main**
   - Folder: **/ (root)**
3. Click **Save**.

---

## Step 3: Wait 1–2 minutes

GitHub will build and deploy. The page will show something like:

**"Your site is live at https://hessi3700.github.io/the-beautiful-ART./"**

(If your repo name has no period at the end, the URL will be without the trailing dot.)

---

## Step 4: Open your site

Open the URL GitHub shows. If you get 404:

- Wait another minute and refresh.
- Make sure **index.html** is in the **root** of the repo (you already have it).
- Try: **https://hessi3700.github.io/the-beautiful-ART./**  
  or **https://hessi3700.github.io/the-beautiful-ART/** (no dot).

---

## If it still says "Actions" or nothing works

- **"Actions is unavailable"**  
  You **must** use **"Deploy from a branch"**, not "GitHub Actions". Your site is static HTML and does not need Actions.

- **Repo name typo**  
  Your remote is `the-beautiful-ART..git` (two dots). If the repo on GitHub is actually **the-beautiful-ART** (one dot or no dot), the URL will match the repo name. Check the repo URL in the browser and use that same name in the Pages URL.

- **Nothing deployed**  
  Push your latest code so that **index.html**, **styles.css**, **script.js**, **.nojekyll**, and the **assets** folder are on the **main** branch. Then in Settings → Pages use **Deploy from a branch** → **main** → **/ (root)** and Save.

---

## Quick checklist

- [ ] Settings → Pages → Source = **Deploy from a branch**
- [ ] Branch = **main**, Folder = **/ (root)**
- [ ] Saved, then waited 1–2 minutes
- [ ] Opened the URL GitHub shows under Pages
