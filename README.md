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

## The line

Two products, drawn from the current tech packs:

| | 200 Quarter | Performance Crew |
|---|---|---|
| Height | Quarter, 5.5" heel to cuff | Mid-crew, 7–7.5" heel to cuff (M) |
| Weight | Midweight cushion | Ultralight |
| Yarn | 58–60% merino / 37–39% nylon (Coolmax®) / 3% elastane | 93% polypropylene / 7% elastane |
| Knit | 168 needle high density | Open mesh, reinforced heel & toe |
| Colorways | 001 Stuart Stone (Stone Heather 415C, Graphite 425C, Larch 7586C) | 001 White/Larch, 002 Black/Larch |
| Origin | USA | TBD |

Larch (Pantone 7586C, `#9E4A28`) is the shared accent: a mountain mark on the
200's cuff, three dashes on the crew's back cuff. Sizes are unisex S/M/L/XL
(US 4–6.5 / 7–9.5 / 10–12.5 / 13–15).

The product art is inline SVG generated from the tech-pack geometry. Colorways
are CSS custom properties set on the `.pshot` wrapper (`--sc`, `--scd`, `--scc`,
`--scm`, `--sca`, plus the texture tokens), so the crew's White/Black toggle is
one `style` swap in JS — no second drawing.

## Before launch

- Prices ($22 / $16) are placeholders — the tech packs don't set them. Confirm before publishing, and update the "$32 sock priced at $22" line in the build section to match.
- Replace the Unsplash placeholder photography with real Teanaway and product shots. Put them in `/public` or an `/img` folder and update the `src` attributes.
- Replace the illustrative SVG socks with real product photography once samples are shot.
- Reviews are placeholder copy — swap in real customer quotes.
- The Performance Crew's country of origin is TBD in the tech pack, so the page makes no origin claim for it. Add one when it's confirmed.
- The "Add to bag" buttons and newsletter form are UI only. Wire them to a real cart (Shopify Buy Button, Snipcart) and an email provider before taking orders.
- Add a `favicon.ico` and an Open Graph image (`og:image` meta tag) for link previews.
