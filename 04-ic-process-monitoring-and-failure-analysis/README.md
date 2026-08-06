# IC Process Monitoring and Failure-Analysis Evidence

This section came from a gap between inspection results and the manufacturing path behind them. Wafer maps and production context were familiar, but the position of WAT parameters such as threshold voltage, saturation current, and contact resistance in the IC process flow was not. The first in-person class connected process layers, scribe-line test structures, wafer-level distributions, CP bins, and later failure analysis. The goal is not to compress all 154 lecture pages into another process textbook. It is to build enough of a map to ask what was measured, what else affects the value, and what evidence is still missing.

## Notes

This section is planned as three short notes:

1. [Process Flow and Evidence Layers](./01-process-flow-and-evidence-layers.md) — a working map from wafer fabrication to WAT, CP, packaging, and final test, with FEOL, MOL, and BEOL kept only to the detail needed for locating evidence.
2. **WAT Test Structures and Yield Signals** — the roles of the product die, scribe line, test key, specification window, wafer-level distribution, and CP yield.
3. **Electrical Anomalies and Process Hypotheses** — a way to move from abnormal threshold voltage, saturation current, sheet resistance, or contact resistance toward a testable hypothesis without calling correlation a root cause.

The detailed process sequence will not be repeated unless it helps answer a practical question: which structure was measured, which process layer may be involved, and what should be checked next.

## What These Notes Connect

The lecture moved from process flow into WAT, wafer maps, specification limits, marginal failures, and CP–WAT correlation. These topics become easier to follow when treated as one evidence chain:

```text
Process step
    ↓
Test structure
    ↓
WAT parameter
    ↓
Wafer-level distribution
    ↓
CP yield or fail bin
    ↓
Failure hypothesis
    ↓
Physical verification
```

The chain can stop early. If only a WAT value and a spatial pattern are available, the result may support a hypothesis, but it does not verify the mechanism.

## A Small Example

Suppose a MOS test structure shows lower-than-expected saturation current. Implantation may be one possibility, but the current also depends on mobility, gate capacitance, channel dimensions, threshold voltage, and measurement conditions. A more useful next step is to confirm repeatability, compare related WAT parameters, inspect the wafer pattern, and then check whether the same region appears in CP fail bins or process records. One low value is a warning. It is not yet a diagnosis.

## Existing Foundations

- [MOS Capacitor C–V and Oxide Charge](../02-semiconductor-characterization-fundamentals/03-mos-capacitor-and-oxide-charge.md) provides the background for gate capacitance, flat-band voltage, and oxide or interface charge.
- [Resistivity, Sheet Resistance, and Four-Point Probe](../03-electrical-characterization-and-process-monitoring/01-resistivity-sheet-resistance-and-four-point-probe.md) separates material resistivity, thin-film sheet resistance, and finished-structure resistance.
- [Contact Resistance and the Transfer Length Method](../03-electrical-characterization-and-process-monitoring/02-contact-resistance-and-transfer-length-method.md) explains why a contact measurement can still contain layer and geometry contributions.

## Future Notes

- Failure-analysis localization workflow
- Material-characterization methods and evidence limits

These notes will be added only after later course material provides enough detail to write them properly.

## Learning Source

1. Personal notes from the first day of an in-person course on integrated-circuit failure analysis and yield improvement, August 6, 2026.

## Note on Scope

I have not operated production WAT or CP equipment, or worked as a semiconductor process-integration engineer. The project connections are limited to experience with wafer-inspection software, especially wafer context, coordinates, recipes, history, and result traceability. Those records can help organize an investigation, but they cannot replace electrical measurement or physical verification. Public notes will use redrawn diagrams and simulated examples rather than original lecture images or confidential production data.
