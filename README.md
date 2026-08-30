# Teanaway Sock Co.

Single-page marketing site for Teanaway Sock Co. (Ellensburg, WA). Static HTML — no build step, no dependencies.

```
.
├── index.html            # the entire site (inline CSS + JS, inline SVG construction drawing)
├── 404.html              # branded not-found page
├── img/                  # product photography
├── og-image.jpg          # 1200x630 link preview card
├── favicon.svg           # the three larch dashes
├── apple-touch-icon.png
├── robots.txt
├── sitemap.xml
├── vercel.json           # clean URLs, security headers, image revalidation
├── .gitignore
└── README.md
```

Everything below the fold of this file is why things are the way they are.
Start with **Before launch** — it is the list of what is still not done.

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

*The Stuart 200 is 5.5" heel to cuff. Its photography is deliberately shot
longer than that so the sock does not read as ankle height — measuring the
shot against the Larch 100 implies 6.3–6.7", which is the render, not the
spec. Do not "correct" the 5.5".*

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

The side views are cut from supplied product photography. **The two black shots
are still cropped from the tech-pack sheet** and are the only low-resolution
images left on the site, so quality drops when someone switches the Larch 100 to
Black.

The back view is the second shot on purpose, and it is framed on the cuff rather
than on the whole sock: shot full-length, the graphite heel is the dominant mass
and the three larch dashes shrink to a detail — the full back view filled 32% of
the frame and the mark was barely legible. Cropping to the cuff with the top of
the heel kept for context takes that to 51% and makes the dashes the subject.
Stray sheet content — annotations, view labels, body copy that fell inside
a crop — was removed by keeping only the sock's
connected pixel region, and each background was lifted to pure white so the
images sit on the page background under `mix-blend-mode: multiply` with no
visible box. Change `--fog` and the frames follow; the photos need no re-export.

Image URLs carry a content hash (`img/name.jpg?v=<sha1[:8]>`), stamped into the
markup by the build step, and `vercel.json` sets `must-revalidate` on `/img/*`.
Both exist because these six filenames get rewritten in place as better
photography arrives — without them a browser or CDN happily serves a months-old
crop, which is exactly what happened once. Re-run the build after replacing any
image so the hash moves.

Side views are saved at native size; the cuff-framed back views are resampled to
1010 px tall, which is what the largest render needs at 2x. JPEG q92, no chroma
subsampling throughout. Every image renders at 0.88–1.09x of its own pixels, so
nothing is being stretched. 632 KB for all six; the black pair only loads if
someone picks that colorway.

The black back view uses a tighter isolation threshold and skips the median pass
the other tech-pack crops use — at the cuff crop's magnification that pass left
a visible white halo around the sock.

Each product has a two-up thumbnail strip that swaps the main image. The Larch
100's colorway buttons swap the whole strip (`.thumbs[data-way]`) and reset it
to the side view. Selecting a view calls `reveal()`, which scrolls the frame
clear of the fixed header if it is sitting underneath it — without that, tapping
the back view on a phone hides the back cuff behind the header, which is the one
thing that shot exists to show.

The only remaining illustration is the seven-callout construction drawing in the
build section, which is inline SVG built from the tech-pack geometry.

## Production status

In place: canonical URL, Open Graph and Twitter cards with a generated
`og-image.jpg`, SVG favicon and apple-touch-icon, `Organization` JSON-LD,
`robots.txt`, `sitemap.xml`, a branded 404, a skip link, one `h1` with no
heading-level skips, alt text on every image, and security plus cache headers
in `vercel.json`.

Removed as unshippable rather than left in place:

- **The customer reviews.** Three quotes with invented initials and towns.
  Fabricated testimonials are a legal problem on a commercial site, not just an
  untidy one. The markup is in git history — restore it the moment there are
  real quotes with permission to use them.
- **The "Added to bag" confirmation.** There is no cart, so nothing should say a
  pair was added. The buttons are left in place and inert, per your call.
- **"You're on the list."** Same reason: nothing was stored. The form now says
  the signup is not connected, and posts properly once you set the endpoint.
- **The footer placeholder note**, and the header **search icon**, which linked
  to the product list and searched nothing.

## Before launch

Blocking:

- **Wire the cart.** The buy buttons and the header bag are inert. Shopify Buy
  Button or Snipcart drop into the existing buttons and size selectors.
- **Wire the newsletter.** Set `SIGNUP_ENDPOINT` at the top of the script block
  in `index.html` to your provider's form endpoint (Formspree, Buttondown,
  Klaviyo). It already validates, posts JSON as `{"email": "..."}`, and handles
  success and failure. Until it is set the form tells the visitor it is not
  connected.
- **Confirm the domain.** `teanawaysockco.com` is assumed by the canonical tag,
  the Open Graph and Twitter URLs, `robots.txt` and `sitemap.xml`. If it is
  different, change it in those four places.
- **Replace the Unsplash landscape photography.** The hero, the mid-page
  feature, the three editorial tiles and the story background are hot-linked
  from `images.unsplash.com`. They are licensed for commercial use, but a live
  storefront depending on someone else's CDN for its hero image is a real
  risk — self-host them, or swap in your own Teanaway shots.
- **Confirm the founder note is your words.** It reads as first person under
  your name in the story section.

Not blocking:

- Both socks are $10. The positioning is that nothing is added to the cost for marketing, which the build section states outright — keep the "$32 sock priced at $10" line in step with the price if it ever moves.
- "Free shipping over $35" in the promo bar is four pairs at $10. Worth a second look now that the price is set.
- **The Larch 100 in Black still needs photography.** The other four shots came from supplied product images; Black is the last pair cropped from a tech-pack sheet, and the drop in quality is visible when the colorway is switched. Two shots, side and back, dropped in over `larch-100-black-side.jpg` and `larch-100-black-back.jpg`, and nothing else has to change.
- **The back-cuff mark disagrees between the photography and the 200 Quarter tech pack.** The photography shows three larch dashes on both socks; the tech pack drew a Mount Stuart mountain on the 200. The site follows the photography and treats the dashes as a house mark. If the mountain is still the intent for the 200, its signature line and the "Three dashes, one range" tile both need reverting.
- Add `Product` JSON-LD with real `offers` once the cart is live. It is deliberately absent now — marking a price and availability on a page that cannot sell would be wrong, and search engines flag it.
- The raw tech-pack sheets are not in this repo. Anything committed here is served publicly by Vercel, and those sheets carry OEM notes — add them only if you want them public.
- The page carries no country-of-origin claim and no third-party brand names, by request. The tech packs list a Coolmax® nylon for the Stuart 200, USA manufacture for it, TBD origin for the Larch 100, and Pantone references for all three colors — none of that appears on the site. Reintroduce any of it only with the licensing and substantiation to back it up.
- "Ships from Ellensburg, Washington" in the promo bar and the Ellensburg lines in the footer and founder note are location and fulfillment, not manufacturing. Say the word if you want those gone too.
