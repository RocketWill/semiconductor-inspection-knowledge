# IC Process Monitoring and Failure-Analysis Evidence

This section started from a gap in how wafer-inspection results fit into the manufacturing path. Wafer maps and production context were familiar, but the position of WAT parameters such as threshold voltage, saturation current, and contact resistance in the IC process flow was not.

The two-day course helped connect those layers. These notes keep only the parts that help ask three questions: what was measured, what else can affect the result, and what evidence should come next.

## Notes

This section contains six notes:

1. [Process Flow and Evidence Layers](./01-process-flow-and-evidence-layers.md) — a working map from wafer fabrication to WAT, CP, packaging, and final test, with FEOL, MOL, and BEOL kept only to the detail needed for locating evidence.
2. [WAT Test Structures and Yield Signals](./02-wat-test-structures-and-yield-signals.md) — the roles of the product die, scribe line, test key, specification window, wafer-level distribution, and CP yield.
3. [Electrical Anomalies and Process Hypotheses](./03-electrical-anomalies-and-process-hypotheses.md) — a way to move from abnormal threshold voltage, saturation current, sheet resistance, or contact resistance toward a testable hypothesis without calling correlation a root cause.
4. [Plasma Etch Monitoring and In-line Inspection](./04-plasma-etch-monitoring-and-inline-inspection.md) — how micro-loading, optical-emission endpoint signals, and spatial defect evidence answer different questions while a plasma etch process is monitored.
5. [Design Rules and Process Margin](./05-design-rules-and-process-margin.md) — why layout dimensions act as an interface between design intent, fabricated geometry, and electrical risk rather than as an isolated DRC checklist.
6. [CP Test Marginality and Shmoo Plots](./06-cp-test-marginality-and-shmoo-plots.md) — how probe contact, timing, and swept test conditions reveal the operating margin hidden by a single nominal pass/fail result.

## What These Notes Connect

The notes connect process conditions to the evidence that appears later in the flow:

```text
Process condition
    ↓
In-line signal / inspection
    ↓
Fabricated geometry
    ↓
WAT distribution
    ↓
CP result
    ↓
Failure hypothesis
    ↓
Physical verification
```

Each layer narrows a different part of the investigation. The next check depends on what the current evidence can actually support.

## Existing Foundations

- [MOS Capacitor C–V and Oxide Charge](../02-semiconductor-characterization-fundamentals/03-mos-capacitor-and-oxide-charge.md) provides the background for gate capacitance, flat-band voltage, and oxide or interface charge.
- [Resistivity, Sheet Resistance, and Four-Point Probe](../03-electrical-characterization-and-process-monitoring/01-resistivity-sheet-resistance-and-four-point-probe.md) separates material resistivity, thin-film sheet resistance, and finished-structure resistance.
- [Contact Resistance and the Transfer Length Method](../03-electrical-characterization-and-process-monitoring/02-contact-resistance-and-transfer-length-method.md) explains why a contact measurement can still contain layer and geometry contributions.

## What Comes Next

This section ends at product-test margin and failure hypothesis. The next section continues with failure localization and physical evidence:

[Failure Localization and Material Characterization](../05-failure-localization-and-material-characterization/README.md)

## Learning Source

1. Hsinchu Science Park Bureau–subsidized course, [*積體電路故障分析技術與良率提升*](https://saturn.sipa.gov.tw/edu/d013_new.jsp?pl_id=26A01&cs_id=15S359) (*IC Failure Analysis Technology and Yield Improvement*, course 15S359), delivered by the Tze-Chiang Foundation of Science & Technology, August 6–7, 2026. Notes 01–03 draw mainly on the first day; notes 04–06 draw on the second day.

## Scope

I have not worked as a semiconductor process-integration or failure-analysis engineer, and I have not operated production plasma-etch, WAT, or CP equipment. My practical connection is mainly wafer-inspection software, including wafer context, coordinates, recipes, history, and result traceability.

The diagrams and examples in this section are simplified conceptual redrawings and do not reproduce lecture slides or production data.
