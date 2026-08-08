# Materials Science

This section records how I rebuilt the materials-science foundation behind some of the inspection problems I had already encountered in industrial computer vision.

The notes begin with material selection, atomic bonding, and crystal structure, then move through defects, diffusion, mechanical failure, processing history, and semiconductor behavior. Across these topics, the same boundary keeps appearing: an inspection image can support a useful observation or hypothesis without identifying the material mechanism behind it.

## Notes

1. [Course Overview](./01-course-overview.md) — The processing–structure–properties–performance framework and how inspection evidence fits into it.
2. [Material Families, Property Trade-offs, and Engineering Selection](./02-material-properties-and-selection.md) — Material families, property trade-offs, engineering selection, and how material choices become inspection constraints.
3. [Atomic Bonding and Crystal Structure](./03-atomic-bonding-and-structure.md) — Valence electrons, bonding, crystal structures, silicon orientation, and the limits of crystallographic hypotheses from optical patterns.
4. [Crystal Defects, Diffusion, and Microstructure](./04-crystal-defects-and-microstructure.md) — Point defects, diffusion, dislocations, grain boundaries, microstructure, and the difference between a material defect and an AI defect label.
5. [Mechanical Properties and Failure Evidence](./05-mechanical-properties-and-failure.md) — Tensile behavior, creep, impact, fracture toughness, fatigue, and why visible geometry is not yet a mechanical failure assessment.
6. [Processing, Phase Transformations, and Material Performance](./06-processing-and-material-performance.md) — Phase diagrams, transformation kinetics, TTT/CCT paths, and the distinction between inspection settings and upstream material history.
7. [Materials-Aware Inspection Evidence](./07-semiconductor-inspection-reflection.md) — Semiconductor carrier behavior, evidence boundaries, inspection context, and a practical structure for connecting optical observations with later verification.

## What These Notes Connect

The section follows a gradual path from material structure to inspection evidence:

```text
Material selection
    ↓
Atomic bonding and crystal structure
    ↓
Defects, diffusion, and microstructure
    ↓
Mechanical response and failure
    ↓
Processing and time–temperature history
    ↓
Semiconductor electrical behavior
    ↓
Inspection evidence and verification
```

The processing–structure–properties–performance relationship remains the materials-science backbone. For inspection work, one more separation is needed:

```text
Optical observation
    ↓
Inspection and product context
    ↓
Engineering hypothesis
    ↓
Electrical / process / material evidence
    ↓
Verified or unresolved conclusion
```

A repeatable image pattern can be useful without identifying an atomic, electrical, mechanical, or process mechanism.

## What Comes Next

This section introduces semiconductor carrier behavior as part of the materials-science course. The next section develops those ideas further through carrier transport, p–n junctions, diode I–V behavior, and MOS capacitor C–V response:

[Semiconductor Characterization Fundamentals](../02-semiconductor-characterization-fundamentals/README.md)

## Learning Source

- James F. Shackelford, [*Materials Science: 10 Things Every Engineer Should Know*](https://www.coursera.org/learn/materials-science), University of California, Davis / Coursera.

## Scope

These are learning notes rather than records of professional materials-characterization or semiconductor-process work.

My practical connection comes from industrial computer vision, AOI, wafer-inspection software, dataset design, optical measurement, and result traceability. I use those experiences to ask what an inspection signal can support, but I do not treat AOI output as proof of crystal structure, a material failure mechanism, semiconductor electrical behavior, or an upstream process root cause.
