# Teanaway Sock Co.

Single-page marketing site for Teanaway Sock Co. (Cle Elum, WA). Static HTML — no build step, no dependencies.

```
.
├── index.html      # the entire site (inline CSS + JS, inline SVG product art)
├── vercel.json     # clean URLs + basic security headers
├── .gitignore
└── README.md
```

## Local preview

Open `index.html` in a browser, or serve it:

```bash
python3 -m http.server 8000
# → http://localhost:8000
```

## Push to GitHub

```bash
git remote add origin https://github.com/<your-username>/teanaway-sock-co.git
git branch -M main
git push -u origin main
```

## Deploy to Vercel

**Dashboard:** vercel.com → Add New → Project → import this repo → Framework Preset **Other**, root directory `./`, leave build and output settings empty → Deploy.

**CLI:**

```bash
npm i -g vercel
vercel        # preview deploy
vercel --prod # production
```

Every push to `main` redeploys automatically once the repo is linked.

## Before launch

- Replace the Unsplash placeholder photography with real Teanaway and product shots. Put them in `/public` or an `/img` folder and update the `src` attributes.
- Replace `[Founder name]` in the founder quote (the "The east slope" section).
- Reviews are placeholder copy — swap in real customer quotes.
- The "Add to bag" buttons and newsletter form are UI only. Wire them to a real cart (Shopify Buy Button, Snipcart) and an email provider before taking orders.
- Add a `favicon.ico` and an Open Graph image (`og:image` meta tag) for link previews.
