# After Hours — locked-room QR puzzle

A single-page escape-room challenge: the QR code encodes `E2G018532A7TP2UWS9`, and the note
above it hints at the four-step decode:

1. **Caesar shift -3** on the letters → `B2D018532X7QM2RTP9`
2. **Take the first half** → `B2D018532`
3. **Reverse it** → `235810D2B`
4. **From base 16 (hex → decimal)** → `9487584555`

Answer: `FLAG{9487584555}`

It's a single static file (`index.html`) — no build step, no server, and no external
dependencies at all. The QR code is a real PNG (`qr-payload.png`, included alongside it)
embedded directly in the page as base64, so it renders identically everywhere and doesn't
rely on any CDN or JavaScript library to generate it.

## Deploy to Vercel

### Option A — Vercel dashboard (no CLI, easiest)

1. Create a new GitHub repo and push this folder to it:
   ```bash
   git init
   git add .
   git commit -m "locked-room QR challenge"
   git branch -M main
   git remote add origin https://github.com/<you>/<repo>.git
   git push -u origin main
   ```
2. Go to [vercel.com/new](https://vercel.com/new) and import that repo.
3. When asked for a framework preset, choose **Other** — no build command, no output
   directory override needed. Vercel will serve `index.html` as-is.
4. Click **Deploy**. You'll get a `*.vercel.app` URL a few seconds later.

### Option B — Vercel CLI (no GitHub needed)

1. Install the CLI once: `npm i -g vercel`
2. From inside this folder, run:
   ```bash
   vercel
   ```
3. Answer the prompts (link to a new project, accept the defaults — it will detect a
   static site automatically).
4. For a production URL: `vercel --prod`

That's it — no `vercel.json` or `package.json` required for a plain static page like
this one.

## Printing the QR code for a physical room

`qr-payload.png` (included in this folder) is the exact same image embedded in the page —
verified to scan back to `E2G018532A7TP2UWS9`. Print that file directly at whatever size
you need for the physical prop; no need to load the page at all.

## Customizing

- **Change the payload / answer:** edit `payload-text` in `index.html` and update
  `ANSWER_DIGITS` in the `<script>` block to match whatever your new decode produces.
- **Change the reveal / twist:** edit the `.reveal` block (caller name, number, and
  closing line) near the bottom of the page.
- **Difficulty:** the note currently spells out all four steps fairly directly. To make
  it harder, vaguen the wording; to make it easier, add a fifth line that names the
  tool ("CyberChef helps").
