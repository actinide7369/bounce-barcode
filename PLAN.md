# Plan, fixed before recording

Fill in the blanks, lock the same plan on the app's Data tab, and upload this file before the first real drop. The GitHub commit time is the public timestamp.

## Question
Which of three known balls did a drop come from, judged only by the sound of its bounces?

## Conditions (chosen before testing)
- Ball A: ____ (marked "A" with tape)
- Ball B: ____ (marked "B")
- Ball C: ____ (marked "C")
- Balls are used as they are; no air is added or let out during the experiment.

## Fixed setup
- Floor: ____ (one taped spot)
- Drop height: 100 cm from the floor to the bottom of the ball, from a taped mark on the wall; released, not thrown
- Phone: on the floor, about 1 m from the spot, screen up, same phone throughout: ____

## Labels
- The label is which ball was dropped. It is decided before each drop and the tape mark is visible on video.
- Optional extra: footprint pressure of each ball (ball pressed onto paper under a known weight, wet patch measured with a ruler; pressure about weight / patch area).

## Recordings and split
- Session S1, references: 6 drops per ball, saved as Reference. These become the grey rows.
- Break of at least 20 minutes.
- Session S2, held-out tests: 4 drops per ball (12 total), order drawn from a cup of 12 slips (4 A, 4 B, 4 C), saved as Held-out test.
- Test drops are never used to draw the reference rows.

## Feature and rule (frozen)
- Feature: bounciness score e = exp(slope of ln(gap) against gap number), first six gaps of at least 45 ms.
- App rule: nearest ball group, boundaries halfway between neighbouring group medians, set from references only.
- Refusal ("No reading"): too few bounces, gaps not shrinking steadily, early and late bounces disagreeing, loose fit, implausible drop height, audio dropout.

## Expected confusion
The two balls with the closest bounciness.

## Reporting
- App rule on the held-out tests: count correct, Wilson 95% interval, confusion table (Data tab).
- Failed drops ("No reading") counted and listed as failure cases.
- Optional: a short reader test with people who have not seen the project.
