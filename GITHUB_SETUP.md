# Open and push AyuSetu from VS Code

## Open the project

1. In VS Code choose **File → Open Folder**.
2. Select this `ayusetu-app` folder.
3. Open **Terminal → New Terminal**.

## Run locally

```bash
python3 -m http.server 4173
```

Open `http://localhost:4173`.

## Push to GitHub

Create an empty repository on GitHub, then run these commands from this folder:

```bash
git remote add origin https://github.com/YOUR-USERNAME/YOUR-REPOSITORY.git
git push -u origin main
```

If GitHub asks for a password, use a GitHub personal access token or authenticate through GitHub Desktop. Never put tokens in source files.

## Deploy from GitHub to Vercel

1. Open https://vercel.com and sign in with GitHub.
2. Choose **Add New → Project**.
3. Import the AyuSetu GitHub repository.
4. Framework preset: **Other**.
5. Build command: leave blank.
6. Output directory: `.`.
7. Click **Deploy**.

Vercel will provide the public URL for the presentation.

## Demo credentials

- Email: `pi@aiia.example`
- Password: `demo`

All data is synthetic demo data. Never use real patient or institutional records in this repository.
