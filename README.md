# Awaken Media — Wall Catalog

A private, map-based catalog of advertising walls inside Yangon's neighbourhoods. Brands sign in with an account issued by Awaken Media, browse 32 townships by price zone, view wall photos, 360° views and traffic data, and build a shortlist ("My walls") that becomes a Waypoints route and an enquiry.

Everything is in one file: `index.html`. Open it in a browser to run it.

## Logins

Demo accounts are defined in `CONFIG.accounts` in `index.html` (hashed). Ask the admin for login details; they are not listed here because this repository is public.

## Adding walls (Admin)

1. Sign in with an admin account → **Admin** tab → **Walls** → **+ Add a new wall**.
2. Press **Drop pin on map** and click the wall's exact spot on the satellite map (or paste latitude/longitude, or use **Use my location** on a phone). The township, Wall ID and nearby stations/landmarks fill in automatically.
3. Fill in the location name, nearest station, size, status, traffic, footfall and notes; add photos and a 360° panorama.
4. **Save**: the wall appears on the map in your browser straight away (marked *Not published*).
5. **Publish** tab → paste a GitHub fine-grained token (this repo only, *Contents: Read and write*) → **Publish**. Photos go to `photos/`, wall data to `walls.json`, and the live site updates for everyone in about a minute.

Wall data lives in `walls.json`. The walls inside `index.html` are only a fallback for offline previews.

## Editing content

All content lives in the `CONFIG` block at the top of the `<script>` in `index.html`:

- `zones` — Zone A/B/C names, traffic, POV, benefit and `price` (MMK per wall per month; `null` shows "On request").
- `walls` — one entry per wall. `lat`/`lon` place the pin exactly; `photos` takes image paths; `pano` takes a 2:1 equirectangular 360° image path (`'demo'` shows the generated sample scene); `detail` holds the full data shown for SAN-001.
- `landmarks` — name, category and approximate `lat`/`lon`.
- `busLines` — schematic corridors; replace with real YBS route geometry.
- `accounts` — prototype accounts (hashed in the browser).

**All wall entries, figures and the SAN-001 detail are dummy data.**

Township boundaries: geoBoundaries (OCHA / MIMU), simplified and embedded as SVG paths.

## Before going live (next steps in Claude Code)

1. **Real sign-in.** The current login runs in the browser and the wall data ships inside the page, so it is not secure. Move accounts and wall data to a backend (e.g. Supabase or Firebase Auth + database) so data is only served after sign-in, and admins create accounts server-side.
2. **Admin console.** Let the field team add walls, upload photos and 360° captures, and set status and prices.
3. **Enquiries.** Send "My walls" enquiries to the team (email/Telegram/Viber or a database) instead of copying to clipboard.
4. **Real data.** Replace dummy walls, verify landmark positions, add real bus routes and zone prices.
5. **Branding.** Swap the placeholder sunrise wordmark for the Awaken Media logo.

## External libraries

- Google Fonts: Oswald, Public Sans
- three.js r128 (cdnjs) — loaded only when a 360° view is opened
