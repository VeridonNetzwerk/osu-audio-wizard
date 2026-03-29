# Troubleshooting

Common problems and quick fixes.

- No sound
  - Make sure the tab is allowed to play audio. Click **Start** to resume the AudioContext.
  - Try a different browser if the sound is missing.

- Clipboard copy fails
  - Opening the file via `file://` may prevent clipboard operations in some browsers. Start a local server:
    ```bash
    npx http-server -c-1
    ```

- Offset seems wrong / too large
  - Ensure you are clicking exactly on the click transient.
  - Close background apps that might create input lag.
  - Try multiple runs and compare medians.

- Result flagged "unreliable"
  - The app shows this when the standard deviation is high (> ~40 ms). Try again with steadier hits.

- Browser doesn't support `audioContext.baseLatency`
  - The app will gracefully fall back (no latency correction). You can still use the reported median but expect small systematic offsets on some setups.
