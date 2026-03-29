# How it Works (technical, but concise)

This page explains the timing model and the math used to compute the offset.

1) Scheduling and time bases
- The app uses the Web Audio API to schedule click sounds with `audioContext.currentTime` (high-precision audio time).
- For matching with user inputs (DOM events), each scheduled beat is mapped to a `performance.now()` target time. That mapping is calculated when the beat is scheduled:

  targetPerf = nowPerf + (beatAudioTime - nowAudio) * 1000

  where `nowPerf = performance.now()` and `nowAudio = audioContext.currentTime`.

2) Input timestamps
- When a key or mouse event occurs, the app uses `event.timeStamp` if available (more accurate for input timing). If missing or unreliable, it falls back to `performance.now()`.

3) Difference calculation
- For each matched input, the raw difference is computed in ms:

  D_raw = input_time_ms - targetPerf

- If the browser reports `audioContext.baseLatency`, the app subtracts that (in ms) as `audioLatencyMs`:

  D = D_raw - audioLatencyMs

4) Matching logic
- Beats are matched deterministically and sequentially: the app keeps a queue of scheduled beats and consumes them in order.
- If the user pauses and misses beats, the scheduler removes missed beats older than a matching window so resumed inputs match the next logical beat instead of being flagged as outliers.

5) Robust statistics
- Initial filter: discard absolute differences greater than ±200 ms.
- Use median() as the robust center measure (resistant to single bad clicks).
- Use MAD (median absolute deviation) to detect and remove additional outliers: compute deviations to the median, take median(deviations) as MAD, and drop samples more than a small multiple of MAD (e.g. 3*MAD, min 10ms).
- Final reported offset = median(filtered_samples) - audioLatencyCorrection.

6) Scheduler details
- A small lookahead (`scheduleAheadSec`, e.g. 0.12s) is used and the scheduler runs frequently (lookAheadMs, e.g. 10ms). The scheduler schedules audio nodes via `AudioBufferSourceNode.start(audioTime)` for accurate output timing.

7) Click sound
- The tool uses a very short noise-burst (windowed) as the click so the transient is easy to perceive and align with.
