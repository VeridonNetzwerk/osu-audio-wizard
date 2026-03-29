# Usage — step by step (idiot‑proof)

This page shows how to use the app in plain language.

1) Open the app
- Recommended: open `index.html` in Chrome, Edge, or Firefox. If you get clipboard errors, serve the folder with a simple HTTP server (`npx http-server`) and open `http://localhost:8080`.

2) Start measuring
- Click **Start**. The app will begin playing short click sounds at a steady BPM (default 120).
- Use `Z` or `X` on your keyboard, or click with the mouse exactly when you hear the click.

3) What to do if you mess up
- If you miss a beat or pause for a few beats, just continue clicking. The tool will skip missed beats and continue measuring the next beats.

4) When the result appears
- After at least 32 valid hits the app computes a robust median offset and displays `Done: Offset +X.XX ms` or marks the result `unreliable` if the variation is high.
- Click **Copy Offset** to copy the value to clipboard and paste into your game's offset setting.

5) Tips for best results
- Use headphones and a keyboard (stable input). Avoid touchpads.
- Try to click exactly on the perceived transient.
- If the result is unreliable, try again and take more steady hits.
