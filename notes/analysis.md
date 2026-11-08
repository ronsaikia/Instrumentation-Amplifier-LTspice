# Analytical notes — three-op-amp instrumentation amplifier

## Design choices

Three UniversalOpAmp2 macro-models; two input op-amps with equal 10 kΩ feedback resistors and a 200 Ω gain-setting resistor; matched 10 kΩ difference amplifier stage; dual 12 V rails.

## Ideal differential gain

For equal first-stage feedback resistors, each of value R, a resistor R_G joining the inverting inputs, and a unit-gain differential second stage:

`|A_d| = (1 + 2 R / R_G) × (R_f/R_in)`.

With `R=10k`, `R_G=200`, and `R_f=R_in=10k`:

`|A_d,ideal|=1 + 2 × 10,000 / 200 = 101 V/V`.

The measured baseline values in the original LTspice log are `V_DIFF,pp = 0.00399999786168 V`, `V_OUT,pp = 0.403958141804 V` and `gain = 100.989589438 V/V`.

Relative gain magnitude error = `(101 - 100.989589438)/101 × 100 = 0.0103075%`.

The saved waveform corresponds to an inversion of output polarity relative to the displayed positive differential-input convention; the above gain is expressed as a **magnitude**.

## CMRR from *archived mismatch run* (not verified on saved schematic)

The archived log says `V_CM,pp = 0.199999958277 V` and `V_OUT,CM,pp = 0.00100000656676 V`.

`|A_cm| = 0.00100000656676 / 0.199999958277 = 0.00500003387687 V/V`.

`CMRR = 20 log10(|A_d/A_cm|) ≈ 86.106 dB`, using `|A_d|=100.989` as in the archived log.

**Caution:** exact modified resistor value/location used by the archived mismatch run isn't recoverable from the saved `.asc` (all four second-stage resistors are saved at 10 kΩ). Therefore these logged numbers are preserved as *archived measurements*, not results of the new explanatory 10.1k schematic.

## What to add next

Repeat CMRR over multiple actual component tolerances using `.step`, sweep frequency using `.ac`, and quantify output saturation and op-amp input offset. Include the `.asc`, measured log, and a summary table for each new claim.
