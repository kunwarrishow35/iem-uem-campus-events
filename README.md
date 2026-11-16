# IEM × UEM Campus Events 2026 — Ignite 2026

A single-file, animated campus events landing page built on the **Kolibrie** motion system.

---

## Running locally

No build step needed. Open `index.html` directly in any modern browser, or serve the folder:

```bash
# Python (any OS)
python -m http.server 8080
# then open http://localhost:8080

# Node (npx)
npx serve .
```

> **Note:** Some browsers block autoplay video even when `muted`. If the hero video doesn't play,
> the page automatically falls back to the poster image with a Ken Burns CSS drift. That is intentional.

---

## Editing the fest name

At the top of the `<script>` block inside `index.html`, find:

```js
const FEST_NAME = 'Ignite 2026';
```

Change the string to whatever you like. The name appears in the nav secondary wordmark,
the footer copyright line, and anywhere else it is referenced.

---

## Editing the EVENTS array

All 12 events live in one `const EVENTS = [ … ]` array near the top of the script.
Each entry looks like this:

```js
{
  id: 'hackhive-36',          // unique slug, used for anchor links and localStorage keys
  title: 'HACKHIVE 36',       // displayed in uppercase on cards
  category: 'Hackathon',      // shown as the category label
  dateStr: '28–29 Nov 2026',  // human-readable date shown on cards
  startDate: '2026-11-28',    // ISO date — used to auto-compute status
  endDate:   '2026-11-29',    // ISO date — used to auto-compute status
  venue: 'Auditorium + Labs', // shown below the date
  time: '10 AM Sat – 10 PM Sun',
  desc: 'Short one-line description shown on the calendar card.',
  img: 'assets/events/hackhive-36.webp',   // relative path to the image
  eligible: true,             // true = shows "Open to IEM and UEM students" badge
  status: 'upcoming',         // fallback only — real status computed from today's date
  tags: ['hackathon'],        // controls which filter pill shows this card
                              // valid tags: 'hackathon','conference','poster',
                              //             'workshop','cultural','sports','robotics'
  stackCard: true,            // true = also appears in the pinned 3D stack (section 2)
  stackFrame: 'butter',       // frame colour: tomato | sky | butter | sage | pink
  stackIndex: 2,              // order in the stack (0 = front)
  linkId: 'card-hackhive-36'  // anchor the stack card links to in the calendar grid
}
```

**Status is computed automatically** from `startDate` / `endDate` vs. the current date at page load.
The `status` field in the array is only used as a fallback if dates are missing.

To add a new event: copy any entry, give it a unique `id`, fill in the fields, and add its image
to `assets/events/`.

---

## Swapping images

All images live in:

```
assets/
  hero/
    uem.png                      ← original new college hero image
    uem.webp                     ← optimized WebP copy for desktop
    uem-1280.webp                ← responsive WebP copy for mobile/tablet
  events/
    hackhive-36.webp
    convergence-summit.webp
    … (12 event images, 4:3 ratio recommended)
  team/
    rishow.jpeg                  ← organiser portrait (Rishow Kunwar, enhanced & color-graded)
    aarav.webp … tanvi.webp      (organiser portraits, ~3:4 ratio)
    setup-crew.webp
    registration-desk.webp
    judges-panel.webp
    late-night-coding.webp
```

Replace any file with your own image at the same path. The page uses `loading="lazy"` and
a `#e9dcc6` background colour as a placeholder, so cards look intentional even before images load.

**Recommended image specs:**
- Events: 800 × 600 px minimum, WebP, ≤ 300 KB each
- Portraits: 600 × 800 px minimum, WebP, ≤ 300 KB each
- Hero poster: 1920 × 1080 px minimum, WebP, ≤ 500 KB

---

## Adding the hero video

If you have a looping MP4 (H.264, no audio, ideally ≤ 10 MB):

1. Save it as `assets/hero/hero-loop.mp4`.
2. The `<video>` tag in `index.html` already points to that path — no code change needed.
3. The browser plays the video; on `prefers-reduced-motion: reduce` it shows only the poster.

If the file is absent, the page shows the poster with a subtle CSS Ken Burns drift. Both paths
coexist and work correctly.

---

## Registration form

The registration modal stores entries **in the browser's `localStorage` only** (key: `iem_registrations`).
No data is sent to any server. This is a demo/prototype. To wire up a real backend, replace the
submit handler (search for `localStorage.setItem('iem_registrations'` in the script) with a `fetch`
to your API endpoint.

---

## Libraries used (CDN)

| Library | Version | Purpose |
|---------|---------|---------|
| GSAP | 3.13.0 | Animation engine |
| ScrollTrigger | 3.13.0 | Scroll-based animations |
| SplitText | 3.13.0 | Character/line text splitting |
| DrawSVGPlugin | 3.13.0 | Animated SVG underlines |
| InertiaPlugin | 3.13.0 | Momentum (flick) hover on team photos |
| Lenis | 1.3.17 | Smooth scroll |

All loaded from `cdn.jsdelivr.net`. The page has a 4-second failsafe: if any library fails to load,
all content becomes immediately visible.

---

## Browser support

Chrome 90+, Firefox 90+, Safari 15+, Edge 90+. Requires JavaScript.

---

*Built for IEM × UEM — Ignite 2026, Kolkata.*

