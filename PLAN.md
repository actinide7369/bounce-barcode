# Plan, fixed before recording (fill in, then commit before the first real drop)

Committed on: ____ (the GitHub commit time is the public timestamp)

## Question
Which pump pressure is this ball at, judged only from the sound of its bounces?

## Conditions (chosen before testing)
- Ball: ____ (printed recommended pressure: ____)
- Levels, by gauge reading: 0.1 bar, 0.3 bar, 0.6 bar (stay inside the range printed on the ball)
- Tolerance when pumping: ± 0.02 bar of the level
- Floor: ____ (one marked spot)
- Drop height: 100 cm to the bottom of the ball, from a taped mark, released not thrown
- Phone position: on the floor, about 1 m from the spot, screen up

## Labels
- Instrument: ____ gauge, resolution ____
- Read the gauge right before each setup, in the same video shot as the ball
- A setup = let air out, pump back to the level, read the gauge. Then 3 drops on that setup.

## Recordings and split
- Reference sessions S1 (Android phone) and S2 (iPhone): 3 setups per level each, 3 drops per setup
- Held-out sessions S3 (Android) and S4 (iPhone), on a different day: 4 setups per level each, 1 drop per setup saved as a held-out test
- Order inside each session: shuffled cards drawn on camera; every level appears equally; redraw if one level bunches up
- Held-out recordings are never used to set reference ranges or thresholds

## Feature and rule (frozen)
- Feature: bounciness score e = exp(slope of ln(gap) against gap number), first six gaps of at least 45 ms
- App rule: nearest group, with boundaries halfway between neighbouring group medians, set from reference sessions only
- Refusal: fewer than 4 bounces, gaps not shrinking steadily (fit below 0.97 or any gap ratio outside 0.3 to 1.05), early and late halves differing by more than 0.08

## Expected confusion
Neighbouring levels (0.3 vs 0.6 bar), because the score flattens at higher pressure.

## Nuisance factors
- Fixed: ball, floor spot, drop height, phone distance
- Varied on purpose across sessions: phone model (Android and iPhone), time of day
- Logged: room temperature, any fan or noise

## Reporting
- App accuracy on held-out sessions: confusion matrix of counts (true level by app answer, plus Refused), with Wilson 95% intervals, Android and iPhone separately
- Reader test: 8 to 10 new readers, forced choice, optional confidence, time per answer
- Failure cases recorded separately: a different floor, a different drop height, a cold ball, a spun drop, a hand-held phone
