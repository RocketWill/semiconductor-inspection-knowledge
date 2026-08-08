# Electrical Characterization and Parameter Extraction

This section started from a fairly simple confusion: resistivity, sheet resistance, contact resistance, and diode series resistance appear in nearby problems, but they do not describe the same part of a structure. The notes begin with four-point-probe measurements, then move to TLM and diode parameter extraction. A short process-monitor bridge marks where parameter extraction ends and process hypotheses begin.

## Notes

1. [Resistivity, Sheet Resistance, and Four-Point Probe](./01-resistivity-sheet-resistance-and-four-point-probe.md) — the difference between material resistivity, thin-film sheet resistance, and the resistance of a finished structure.
2. [Contact Resistance and the Transfer Length Method](./02-contact-resistance-and-transfer-length-method.md) — current crowding, transfer length, and the assumptions behind separating layer and contact resistance.
3. [Diode Parameter Extraction and Measurement Limits](./03-diode-parameters-and-process-monitoring.md) — saturation current, ideality factor, series resistance, fitting limits, and a short bridge to process monitoring.

## What I Am Trying to Separate

The three notes deal with different measurements, but the same problem keeps appearing: a measured value usually contains more than one contribution.

- Material resistivity is not the same as the resistance of a patterned structure.
- Semiconductor layer resistance and metal–semiconductor contact resistance need to be separated.
- Junction behavior and diode series resistance dominate different parts of an I–V curve.
- A process-monitor warning can support an investigation, but it is not yet a verified root cause.

Once I stopped treating these quantities as interchangeable, the formulas became easier to follow, and so did the limits of each measurement.

## Learning Source

1. Arizona State University, [*Electrical Characterization: Diodes*](https://www.coursera.org/learn/electrical-characterization-diodes), Coursera.

## Note on Scope

I have not carried out four-point-probe or TLM measurements in a production characterization role. The project connections in these notes are limited to habits carried over from wafer-inspection software: keeping a value linked to its wafer context, measurement conditions, spatial position, history, and later verification.
