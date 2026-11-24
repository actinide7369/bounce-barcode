# Bounce Barcode

A phone web app that tells balls apart by how bouncy they are, measured from the sound of their bounces.

Open it in Chrome or Safari on any phone: **https://actinide7369.github.io/bounce-barcode/** (link live once uploaded to GitHub Pages).

Built for ED5518 Data Visualization for Engineers, IIT Madras, Project 2, Challenge 5: measure a real physical condition with a phone sensor, and make a visual that helps another person identify the condition from new, held-out recordings.

## What it measures

When a ball lands it keeps a fraction e of its speed (the coefficient of restitution, shown as the "bounciness score"). Flight time is proportional to speed, so each gap between bounce sounds is e times the gap before. The app:

1. records the microphone (echo cancellation, noise suppression and auto gain requested off),
2. high-pass filters at 250 Hz to drop hum and rumble,
3. finds the sharp start of each bounce from its broadband click (1.5 kHz band, 1 ms envelope, sample-level onset), so a ringing ball's beats can't fake a bounce,
4. tries every start and keeps the run of sounds whose gaps shrink most steadily, ignoring echoes and stray knocks,
5. fits a straight line to log(gap) against gap number over the first six gaps; the slope gives e,
6. refuses to score when too few bounces are heard, the gaps don't shrink steadily, early and late bounces disagree, the fit is loose, the implied drop height doesn't fit, or audio dropped out.

More air pressure makes a ball springier, so e rises with pressure; the ball's build matters too. The score uses timing only; loudness matters just for whether each bounce is heard.

## The visual

- **Bounce rhythm (barcode comparator).** One row per reference ball. Grey ticks are reference drops, one tick per bounce. The recording being judged is orange and repeated in every row. Time is scaled by the first gap, so drop height cancels out.
- **Bounciness score strip.** Every drop is a dot on one shared axis. Reference ranges for each ball are shaded and labelled, split halfway between neighbouring groups. The judged recording is one orange line.

Orange always means the recording being judged; grey always means references.

## The experiment

1. **Plan (locked before any drop):** three different balls marked A, B and C, one floor spot, one drop height (100 cm), one phone position. See `PLAN.md`.
2. **References:** each ball dropped several times and saved. These are the grey rows, the answer key.
3. **Held-out tests:** the balls dropped again in an order drawn from a cup, saved as tests. The app hides which ball each was and gives them opaque codes (like `T7KQ`).
4. **Readers:** someone new looks at each test drop on the Compare tab and picks the ball; picks are checked against `c5_test_truth.csv`, which is in the submission ZIP and not on this website.

The label of each drop is which ball was dropped, decided before the drop and visible on the video, so it does not depend on the app. Balls differ in bounciness through their air pressure and build.

## For graders

1. Watch the one-minute video.
2. Open the Compare tab; for each test code pick the ball whose grey row matches the orange barcode, or run the reader test. Check against `c5_test_truth.csv`.
3. Try Check with any ball, or the one-tap self-tests on the Test tab.
4. About explains the physics, labels, limits and course links.

## How to check it works

- **Known-bounce check:** Test tab, play a test bounce of known score from a laptop while the phone listens. The phone should read the same score within 0.01.
- **Tape check:** the app estimates drop height from the first gap. Compare with a tape measure.
- **Sound file:** record a drop with any voice recorder and use "Analyse a sound file".
- **Self-tests:** Test tab, one tap each: a clean drop, a knock before the drop, a knock between bounces, only three bounces, and knocks with no ball, each with the expected result.
- **Example data:** Test tab, simulated references and tests (clearly marked, never exported) to try every screen without a ball.

Automated tests (Playwright, headless Chrome with a fake microphone) feed independent synthetic recordings through the real browser audio path: three bounciness levels, a different drop height, a noisy room with speech, fan, hum, echo and reverb, a ringing ball, a knock before the drop, a slow drop after a stray sound, 44.1 kHz audio, plus silence and random knocks that must be refused (13 recordings, 26 of 26 passing over two repeats). A 24-step flow test covers file upload, the known-bounce sound, saving references and tests, the three exports (with no test labels in the site data), the reader test, the self-tests and the held-out accuracy panel. An attack set of about 450 synthetic recordings (stray knocks, ringing balls, hum, reverb, knocks with no ball) read every clean drop correctly; 5 knock-only recordings still got a score. All of this is on synthetic sound; the real-phone check is the known-bounce test and real drops.

## Files

- `index.html`: the whole app (no external libraries, works offline once loaded).
- `data/bounce_data.json`: published reference and test recordings (bounce times and scores only, no audio, no test labels).
- `PLAN.md`: the plan fixed before recording.
- `c5_test_truth.csv` (submission ZIP only): the true ball for each test code.

## Course links (ED5518)

Decision first (W4, W8); position on a common scale (W2, Cleveland and McGill); one highlight colour against grey (W2); comparison against every condition at once (W3); tested envelope versus a rule set on a different floor (W5, midsem Q11); refuse beyond the evidence (W5 Draupner, W6 silent failure); every summary is a selection (W7); verification by known inputs, held-out data and a blind reader test (W9).
