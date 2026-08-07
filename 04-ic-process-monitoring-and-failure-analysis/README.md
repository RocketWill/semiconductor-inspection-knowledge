# IC Process Monitoring and Failure-Analysis Evidence

This section came from a gap between inspection results and the manufacturing path behind them. Wafer maps and production context were familiar, but the position of WAT parameters such as threshold voltage, saturation current, and contact resistance in the IC process flow was not. The first day of the course connected process layers, scribe-line test structures, wafer-level distributions, CP bins, and later failure analysis. The second day added process-time signals, in-line defect evidence, and the margin between a layout target and fabricated geometry. The goal is not to turn the course into another process textbook. It is to build enough of a map to ask what was measured, what else affects the value, and what evidence is still missing.

## Notes

This section contains six notes:

1. [Process Flow and Evidence Layers](./01-process-flow-and-evidence-layers.md) — a working map from wafer fabrication to WAT, CP, packaging, and final test, with FEOL, MOL, and BEOL kept only to the detail needed for locating evidence.
2. [WAT Test Structures and Yield Signals](./02-wat-test-structures-and-yield-signals.md) — the roles of the product die, scribe line, test key, specification window, wafer-level distribution, and CP yield.
3. [Electrical Anomalies and Process Hypotheses](./03-electrical-anomalies-and-process-hypotheses.md) — a way to move from abnormal threshold voltage, saturation current, sheet resistance, or contact resistance toward a testable hypothesis without calling correlation a root cause.
4. [Plasma Etch Monitoring and In-line Inspection](./04-plasma-etch-monitoring-and-inline-inspection.md) — how micro-loading, optical-emission endpoint signals, and spatial defect evidence answer different questions while a plasma etch process is monitored.
5. [Design Rules and Process Margin](./05-design-rules-and-process-margin.md) — why layout dimensions act as an interface between design intent, fabricated geometry, and electrical risk rather than as an isolated DRC checklist.
6. [CP Test Marginality and Shmoo Plots](./06-cp-test-marginality-and-shmoo-plots.md) — how probe contact, timing, and swept test conditions reveal the operating margin hidden by a single nominal pass/fail result.

The detailed process sequence will not be repeated unless it helps answer a practical question: which structure was measured, which process layer may be involved, and what should be checked next.

## What These Notes Connect

Across the two course days, the section moved from process flow and process-time signals into fabricated geometry, in-line inspection, WAT distributions, CP results, and later verification. These topics become easier to follow when treated as one evidence chain:

```text
Process condition
    ↓
Process-time signal
    ↓
Fabricated geometry
    ↓
In-line measurement or inspection
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

The chain can stop early. An endpoint shift, a visible defect, a design-rule violation, a WAT value, and a CP fail bin belong to different evidence layers. Any one of them may narrow the next check, but none should be promoted directly to a verified mechanism.

## Existing Foundations

- [MOS Capacitor C–V and Oxide Charge](../02-semiconductor-characterization-fundamentals/03-mos-capacitor-and-oxide-charge.md) provides the background for gate capacitance, flat-band voltage, and oxide or interface charge.
- [Resistivity, Sheet Resistance, and Four-Point Probe](../03-electrical-characterization-and-process-monitoring/01-resistivity-sheet-resistance-and-four-point-probe.md) separates material resistivity, thin-film sheet resistance, and finished-structure resistance.
- [Contact Resistance and the Transfer Length Method](../03-electrical-characterization-and-process-monitoring/02-contact-resistance-and-transfer-length-method.md) explains why a contact measurement can still contain layer and geometry contributions.

## What Comes Next

The current section now reaches from process evidence to product-test margin. Detailed failure localization and material-characterization evidence will move into a separate section rather than turning this README into an instrument survey.

The source material for that next section is available from the second course day. Articles will be added only after each topic has been checked against the existing notes and reduced to one engineering question.

## Learning Source

1. Hsinchu Science Park Bureau–subsidized course, [*積體電路故障分析技術與良率提升*](https://saturn.sipa.gov.tw/edu/d013_new.jsp?pl_id=26A01&cs_id=15S359) (*IC Failure Analysis Technology and Yield Improvement*, course 15S359), delivered by the Tze-Chiang Foundation of Science & Technology, August 6–7, 2026. Notes 01–03 draw mainly on the first day; notes 04–06 draw on the second day.

## Note on Scope

I have not operated production plasma-etch, WAT, or CP equipment; defined foundry design rules or production test programs; or worked as a semiconductor process-integration or failure-analysis engineer. The project connections are limited to experience with wafer-inspection software, especially wafer context, coordinates, recipes, history, and result traceability. Those records can help organize an investigation, but they cannot replace electrical measurement or physical verification. Public notes use redrawn diagrams and conceptual examples rather than original lecture images or confidential production data.
