# Futuristic email countdown — 17 Nov 2026

Email clients block JavaScript, so a live countdown has to be an image that is
generated at the moment the email is opened. This tiny server does exactly that:
every request to `/countdown.gif` returns a 60-second animated GIF starting from
the real time remaining.

## Deploy (Vercel, ~5 minutes)
1. Put this folder in a GitHub repo (or run `npx vercel` inside it).
2. Import the repo at vercel.com → New Project → Deploy (no settings needed).
3. Open `https://<your-project>.vercel.app/countdown.gif` in a browser to check it.
4. In `hubspot-snippet.html`, replace `YOUR-PROJECT` with your Vercel subdomain.

## Add to HubSpot
Marketing email editor → drag in a **Rich text** module → click the **Source code**
(`</>`) button → paste the snippet → Save. Send yourself a test and open it in
Gmail, Outlook and Apple Mail. Then check that the image `src` in the received
email still points to your Vercel URL (not a HubSpot CDN copy), since a copied
image would be frozen.

## Customise
All settings are at the top of `api/_countdown_render.py`:
- `TARGET` — currently 17 Nov 2026, 00:00 IST (UTC+5:30)
- `TARGET_LABEL`, `HEADER_LABEL`, `DONE_LABEL` — on-image text
- colour constants (`CYAN`, `MAGENTA`, `BG` …)

After the target passes, the image shows 00:00:00:00 and "WE ARE LIVE".

## Notes
- Outlook for Windows shows only the first frame of a GIF; that frame is still
  accurate at open time, it just won't tick.
- Some clients (e.g. Gmail) proxy images; the time shown is correct at open, but a
  reopen may show a cached copy.
- GIF is ~400 KB. Fonts: Orbitron & Share Tech Mono (SIL Open Font License).
