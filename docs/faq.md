# FAQ

Q: Why use median instead of mean?

A: Median resists single bad clicks and gives a stable center even when a few samples are off.

Q: Can I change BPM?

A: Yes — edit the `BPM` constant at the top of `index.html`.

Q: Why a noise click?

A: A short noise burst produces a sharp transient that is easier to align with than a smooth sine.

Q: I paused and resumed; why were some clicks ignored?

A: The app removes missed beats older than the matching window so resumed clicks match the next scheduled beat; if a click is too far from the next beat it will be treated as "no match".

Q: Can you add CI or automated tests?

A: Yes — we can add lightweight HTML/JS linting or a small Node test harness. Tell me if you want this.
