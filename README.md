# Teanaway Sock Co.

Single-page marketing site for Teanaway Sock Co. (Cle Elum, WA). Static HTML — no build step, no dependencies.

```
.
├── index.html      # the entire site (inline CSS + JS, inline SVG construction drawing)
├── img/            # product photography, cropped from the V1 tech-pack sheets
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

| | Stuart 200 | Larch 100 |
|---|---|---|
| Height | Quarter, 5.5" heel to cuff | Mid-crew, 7–7.5" heel to cuff (M) |
| Weight | Midweight cushion | Ultralight |
| Yarn | 58–60% merino / 37–39% nylon / 3% elastane | 93% polypropylene / 7% elastane |
| Knit | 168 needle high density | Open mesh, reinforced heel & toe |
| Colorways | Stuart Stone (Stone Heather, Graphite, Larch) | White/Larch, Black/Larch |
| Back-cuff mark | Mount Stuart, in larch | Three larch dashes |

Both are performance socks, so the names carry the place and the cushion weight
rather than the fibre — the tech packs' "merino" and "performance" labels would
not have told a customer them apart. Each sock is named for the mark on its own
back cuff, and the number is the cushion weight, continuous with the old
100/200/300 line. Larch (`#9E4A28`) is the shared accent. Sizes are unisex
S/M/L/XL (US 4–6.5 / 7–9.5 / 10–12.5 / 13–15).

Product copy carries the name alone — no colorway numbers, version codes or
rank badges, and nothing overlaid on the photography.

### Product imagery

`img/` holds six shots cropped out of the two tech-pack sheets — two per sock,
side and back:

```
stuart-200-side.jpg        larch-100-white-side.jpg   larch-100-black-side.jpg
stuart-200-back.jpg        larch-100-white-back.jpg   larch-100-black-back.jpg
```

The back view is the second shot on purpose: it is where each sock's mark sits,
over the heel. Sheet annotations — the 5.5" dimension line, the view labels,
body copy that fell inside the crop — were removed by keeping only the sock's
connected pixel region, and each background was lifted to pure white so the
images sit on the page background under `mix-blend-mode: multiply` with no
visible box. Change `--fog` and the frames follow; the photos need no re-export.

Each product has a two-up thumbnail strip that swaps the main image. The Larch
100's colorway buttons swap the whole strip (`.thumbs[data-way]`) and reset it
to the side view.

The only remaining illustration is the seven-callout construction drawing in the
build section, which is inline SVG built from the tech-pack geometry.

## Before launch

- Prices ($22 / $16) are placeholders — the tech packs don't set them. Confirm before publishing, and update the "$32 sock priced at $22" line in the build section to match.
- Replace the Unsplash placeholder landscape photography with real Teanaway shots and update the `src` attributes.
- The product shots in `img/` are cropped from the tech-pack sheets and show development samples. Native crops top out at 295 x 455 px (the Stuart 200 side view) and 111 x 257 px (its back view); they ship resampled 2x with Lanczos and a light unsharp so browsers are not left to upscale them, but the detail is not really there. Reshoot at full resolution before launch and drop the new files in over the same filenames.
- The raw tech-pack sheets are not in this repo. Anything committed here is served publicly by Vercel, and those sheets carry OEM notes — add them only if you want them public.
- Reviews are placeholder copy — swap in real customer quotes.
- The page carries no country-of-origin claim and no third-party brand names, by request. The tech packs list a Coolmax® nylon for the Stuart 200, USA manufacture for it, TBD origin for the Larch 100, and Pantone references for all three colors — none of that appears on the site. Reintroduce any of it only with the licensing and substantiation to back it up.
- "Ships from Ellensburg, Washington" in the promo bar and the Ellensburg lines in the footer and founder note are location and fulfillment, not manufacturing. Say the word if you want those gone too.
- The "Add to bag" buttons and newsletter form are UI only. Wire them to a real cart (Shopify Buy Button, Snipcart) and an email provider before taking orders.
- Add a `favicon.ico` and an Open Graph image (`og:image` meta tag) for link previews.
