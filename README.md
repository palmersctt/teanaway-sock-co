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
| Back-cuff mark | Three larch dashes | Three larch dashes |

Both are performance socks, so the names carry the place and the cushion weight
rather than the fibre — the tech packs' "merino" and "performance" labels would
not have told a customer them apart. The number is the cushion weight,
continuous with the old 100/200/300 line. Larch (`#9E4A28`) is the shared
accent. Sizes are unisex S/M/L/XL (US 4–6.5 / 7–9.5 / 10–12.5 / 13–15).

The three larch dashes are a house mark, not a per-sock one: the supplied
product photography shows them on the back cuff of both socks. The 200 Quarter
tech pack drew a Mount Stuart mountain there instead, so the two disagree — the
site follows the photography. See the launch list.

Product copy carries the name alone — no colorway numbers, version codes or
rank badges, and nothing overlaid on the photography.

### Product imagery

`img/` holds six shots — two per sock, side and back:

```
stuart-200-side.jpg        larch-100-white-side.jpg   larch-100-black-side.jpg
stuart-200-back.jpg        larch-100-white-back.jpg   larch-100-black-back.jpg
```

The first four are cut from supplied product photography and are native
resolution — 661 x 784 up to 581 x 877. **The two black shots are still cropped
from the tech-pack sheet** and are the only low-resolution images left on the
site, so quality drops visibly when someone switches the Larch 100 to Black.

The back view is the second shot on purpose: it is where the mark sits, over the
heel. Stray sheet content — annotations, view labels, body copy that fell inside
a crop — was removed by keeping only the sock's
connected pixel region, and each background was lifted to pure white so the
images sit on the page background under `mix-blend-mode: multiply` with no
visible box. Change `--fog` and the frames follow; the photos need no re-export.

The photographed four are saved at native size, JPEG q92, no chroma
subsampling. The two black shots, having no better source, are resampled 3x
(Lanczos, a median pass to kill the ringing that introduces, then unsharp) at
q95. Every image renders at roughly 1x on a 3x phone. 496 KB for all six; the
black pair only loads if someone picks that colorway.

Each product has a two-up thumbnail strip that swaps the main image. The Larch
100's colorway buttons swap the whole strip (`.thumbs[data-way]`) and reset it
to the side view. Selecting a view calls `reveal()`, which scrolls the frame
clear of the fixed header if it is sitting underneath it — without that, tapping
the back view on a phone hides the back cuff behind the header, which is the one
thing that shot exists to show.

The only remaining illustration is the seven-callout construction drawing in the
build section, which is inline SVG built from the tech-pack geometry.

## Before launch

- Prices ($22 / $16) are placeholders — the tech packs don't set them. Confirm before publishing, and update the "$32 sock priced at $22" line in the build section to match.
- Replace the Unsplash placeholder landscape photography with real Teanaway shots and update the `src` attributes.
- **The Larch 100 in Black still needs photography.** The other four shots came from supplied product images; Black is the last pair cropped from a tech-pack sheet, and the drop in quality is visible when the colorway is switched. Two shots, side and back, dropped in over `larch-100-black-side.jpg` and `larch-100-black-back.jpg`, and nothing else has to change.
- **The back-cuff mark disagrees between the photography and the 200 Quarter tech pack.** The photography shows three larch dashes on both socks; the tech pack drew a Mount Stuart mountain on the 200. The site follows the photography and treats the dashes as a house mark. If the mountain is still the intent for the 200, its signature line and the "Three dashes, one range" tile both need reverting.
- The Stuart 200 in the supplied photography reads lower than the tech pack's drawing of it. Worth confirming the `Quarter · 5.5" heel to cuff` spec still matches the sample being shot.
- The raw tech-pack sheets are not in this repo. Anything committed here is served publicly by Vercel, and those sheets carry OEM notes — add them only if you want them public.
- Reviews are placeholder copy — swap in real customer quotes.
- The page carries no country-of-origin claim and no third-party brand names, by request. The tech packs list a Coolmax® nylon for the Stuart 200, USA manufacture for it, TBD origin for the Larch 100, and Pantone references for all three colors — none of that appears on the site. Reintroduce any of it only with the licensing and substantiation to back it up.
- "Ships from Ellensburg, Washington" in the promo bar and the Ellensburg lines in the footer and founder note are location and fulfillment, not manufacturing. Say the word if you want those gone too.
- The "Add to bag" buttons and newsletter form are UI only. Wire them to a real cart (Shopify Buy Button, Snipcart) and an email provider before taking orders.
- Add a `favicon.ico` and an Open Graph image (`og:image` meta tag) for link previews.
