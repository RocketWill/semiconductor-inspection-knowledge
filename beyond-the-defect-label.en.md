# Beyond the Defect Label

[中文版](./beyond-the-defect-label.md)

## From Optical Inspection Signals to Testable Investigation Hypotheses

> **Engineering Synthesis**
>
> The earlier notes examined materials, semiconductor electrical behavior, process monitoring, and failure analysis as separate subjects. By the end, those subjects had started to connect. They also raised a more practical question: if I receive a new wafer inspection signal, what should I check next? What evidence would give me a reason to change my current interpretation?
>
> The illustrative scenario below is designed to work through that judgment. Its wafer maps, measurement results, and evidence updates are conceptual. They do not represent customer data, a production case, or failure analysis that I performed.

## 1. Do Not Name the Signal Too Early

Suppose AOI repeatedly reports a low-contrast, edge-region optical anomaly on several wafers that share the same production context. The signal is concentrated on the same side of each wafer, although its extent and intensity vary.

![A synthetic wafer map showing a recurring low-contrast optical signal near the wafer edge](./assets/beyond-the-defect-label/02-synthetic-wafer-map.svg)

> Figure 1: A synthetic wafer map showing only that several wafers contain an optical signal in a comparable edge region. The locations, counts, and distributions are conceptual. No electrical result, material mechanism, or process cause has been assigned.

The first instinct is often to reach for a defect name. Is this haze, residue, or a change left by an edge-related process? But once the name is attached, classification and cause can slip into the observation with it. At this point, the evidence says much less: under a specified acquisition condition, the images contain a repeatable low-contrast region whose spatial distribution is not entirely random.

I would first retain the raw image, wafer orientation, coordinates, camera, illumination, exposure, ROI, recipe, preprocessing, model version, and threshold. I would also record the frequency and extent of the anomaly on each wafer. If the signal comes from whole-image classification, it should remain separate from a bounding box or segmentation mask. A wafer-level appearance and a localized object have different annotation semantics. A confidence score does not make them the same kind of evidence.

At this stage, I still cannot claim that the wafer contains a material anomaly. The more accurate statement is narrower: the inspection system observed a signal, and the acquisition context that produced it is known.

## 2. Check Whether the Observation Holds Up

In inspection-system work, class, confidence, and detection results naturally attract attention first. When a low-contrast signal also sits near an optical boundary, however, the acquisition conditions need attention before another defect label is created.

I would begin by repeating the acquisition on the same wafer or on a controlled reference sample. Then I would vary the illumination direction, exposure, or image-processing settings within a reasonable range. If the anomaly moves with an ROI boundary, stitching position, camera channel, or a particular recipe version, the problem may still lie in the inspection chain. An error in wafer orientation or coordinate transformation can also produce an edge cluster that looks surprisingly stable after several wafer maps are overlaid.

The purpose is not to prove that the anomaly is “only a software problem.” It is to check whether the observation can be reproduced. If the raw image does not contain the same change and only the model output shifts, I would return to the threshold, training distribution, and preprocessing. But if the signal remains at the same physical location after the acquisition conditions change, wafer-related variation becomes a more reasonable direction to investigate.

### First Evidence Update

Assume that the anomaly remains visible under another illumination setup and an independent acquisition path. Its location still maps to the same wafer-edge region. The contrast changes, but the signal does not move with the camera channel or ROI boundary.

This result weakens an explanation based on a single camera, recipe, or coordinate artifact. It does not close the gap between “reproducible on the wafer” and “confirmed material change.” The result still does not separate surface geometry from film response, contamination, handling marks, or other possibilities.

## 3. Do Not Keep Only the Most Convenient Explanation

It is easy to keep the explanation that already feels most likely, then use later measurements to look for supporting evidence. The problem is that even a matching image may not show whether the other possibilities have actually been excluded.

I would keep several competing hypotheses that the next check could distinguish. They are not necessarily mutually exclusive. A surface variation may appear together with a particular production context or electrical distribution. Keeping them separate helps show which explanation becomes weaker when new evidence arrives.

| Current hypothesis | Why it cannot yet be excluded | What would weaken it |
| --- | --- | --- |
| Residual acquisition or alignment artifact | Independent acquisition has weakened this direction, but raw-image consistency, coordinate registration, and a different acquisition path have not all been checked | A different acquisition path maps the signal to the same physical location, with consistent raw images and coordinate registration |
| Wafer surface-related variation | The signal remains reproducible under different acquisition conditions | Independent surface inspection finds no corresponding morphology or contrast |
| Spatial variation associated with production context | Several wafers show a similar edge distribution | No repeatable grouping remains after comparison by lot, time, or equipment context |
| Possible electrical spatial correlation | The optical distribution may overlap a region containing marginal dies | No consistent electrical distribution appears after alignment, or the apparent correlation exists only when groups are pooled |

The last row is the least certain because the scenario does not yet contain electrical evidence. An optical anomaly can be a real wafer variation and still have no observable electrical impact. Forcing a WAT parameter into the analysis simply to complete the evidence chain may connect results that do not belong together.

## 4. The Next Check Should Move the Judgment Forward

I originally found it easy to picture failure-analysis methods as a fixed sequence: AOI, then SEM, followed by EDS, FIB, and TEM. The order looks less fixed here. A more useful question is which two explanations most need to be separated now.

![An investigation workflow connecting optical-signal validation, competing hypotheses, and discriminating evidence](./assets/beyond-the-defect-label/01-investigation-logic.svg)

> Figure 2: An evidence-update loop rather than a standard production failure-analysis flow. Electrical, localization, and material evidence are selected according to the question. The diagram does not imply a fixed sequence or claim that I have operated the associated equipment.

If it is still unclear whether the signal follows the wafer, repeating the acquisition, preserving raw data, and comparing recipe and software history are closer to the current question than requesting destructive analysis. Once the signal has been tied to the wafer, the next step depends on the remaining gap. If the question concerns surface morphology, an independent surface inspection or SEM verification request may help. If the next question concerns elemental composition, EDS becomes relevant, while interaction volume, background, and peak overlap still need to be considered. `Contrast ≠ composition`.

If the optical anomaly may align with an electrical distribution, I would first check wafer orientation, coordinate transformation, sampling density, lot grouping, and test conditions. Overlap between WAT or CP maps can raise the priority of a hypothesis, but spatial overlap remains a correlation. The related reasoning is discussed in [WAT Test Structures and Yield Signals](./04-ic-process-monitoring-and-failure-analysis/02-wat-test-structures-and-yield-signals.md), [Electrical Anomalies and Process Hypotheses](./04-ic-process-monitoring-and-failure-analysis/03-electrical-anomalies-and-process-hypotheses.md), and [CP Test Marginality and Shmoo Plots](./04-ic-process-monitoring-and-failure-analysis/06-cp-test-marginality-and-shmoo-plots.md).

If the abnormality can be reproduced under a specified bias, EMMI may help narrow the location of the electrical activity. A hotspot still does not name the physical defect. If the remaining question concerns a buried interface or subsurface structure, I would then consider whether a targeted FIB cross-section or TEM preparation could answer it. A single cross-section cannot reconstruct the causal process history. `Localization ≠ diagnosis`.

## 5. How New Results Change the Earlier Explanations

The first round weakened the acquisition-artifact explanation. If electrical data can be aligned, the next comparison is whether the optical distribution and electrical marginality vary together. I should not assume that a correlation will exist, and I should not pool every lot simply to obtain a clean-looking trend. Once the data are split back into individual lots, an apparently clear direction may turn out to be driven by only one group. At that point, what changes first is the reading of the correlation, not the material explanation.

### Second Evidence Update

Now assume that the wafer group with the more visible edge anomaly also contains more electrically marginal dies in a nearby region. After separating the data, however, this relationship appears in only one lot. The other lots have weaker optical signals and do not show the same electrical distribution.

This further weakens the idea that one inspection setting explains the whole pattern. Wafer-related variation and its association with a particular production context deserve more attention. The optical distribution may also relate to electrical marginality. But the lot-specific factor is still mixed in. The material mechanism, process step, and causal direction remain unknown.

The tempting shortcut is to compress “same lot, nearby location, same direction” into “a process caused the electrical failure.” Too much is still missing: measurement repeatability, sampling coverage, other shared variables, and physical evidence that can separate surface, composition, and subsurface structure. Matching maps narrow the investigation. They do not finish it.

### Third Evidence Update

Finally, add one conceptual result: independent surface inspection finds a reproducible morphology difference in the same edge region. No composition-sensitive evidence is available yet.

The surface-related hypothesis now looks more reasonable, while an explanation based on electrical variation with no corresponding surface change becomes weaker. The morphology difference may feel close to material evidence, but it does not identify the chemical composition or the process step that formed it. If candidate elements become the next question, EDS may add another evidence layer. If the question lies at a buried interface, even a clear surface image may need more precise localization before a cross-section is worth considering.

After these three updates, the difference between “one more data point” and “one more discriminating data point” becomes clearer. A new measurement may produce another similar-looking image without weakening any candidate explanation. In that case, I still need to ask how much information it added.

## 6. Where the Evidence Currently Stops

At this point, the synthetic scenario supports a limited statement: the edge-region optical anomaly remains reproducible under independent acquisition, shows an association worth investigating with a particular production context and localized electrical marginality, and corresponds to a surface morphology difference in the same region.

The chemical composition of the anomaly is still unknown. So is whether the buried interface contains a structural change or which process produced the observations. The current evidence does not establish a causal direction between the optical, surface, and electrical results. This is not a verified root cause.

Any further verification request should depend on which remaining hypothesis most needs to be separated. Composition evidence, a cross-section, and more precise electrical localization answer different questions; the scenario does not need all of them simply to feel complete. When the available data cannot support a more specific cause, `unresolved` is more accurate than a defect name assigned too early.

## 7. How This Changes the Order of Judgment in Inspection Work

In earlier inspection projects, it was easy for the endpoint to be detection rate, classification results, measurement stability, or model deployment. Those tasks still matter. Without a stable observation, the later analysis has no foundation.

Now I also ask where an output sits in the evidence chain. Is it a raw observation, a classification that already contains a hypothesis, a reproducible measurement, a correlation across datasets, or a cause supported by independent evidence? Each level requires different records, and the wording of confidence should change with it.

The order that now feels more useful is to validate the observation, retain competing hypotheses, and select evidence that can separate them. New results should change the earlier judgment. Where the investigation stops depends not on the number of methods, but on how far the evidence actually reaches.

This scenario does not arrive at a material root cause. What remains is closer to a verification-request map: which checks have weakened an explanation, which associations appear only within a particular grouping, and what the next evidence must answer before the judgment can move forward.

## Related Notes

- [Materials-Aware Inspection Evidence](./01-materials-science/07-semiconductor-inspection-reflection.md)
- [From Process Flow to Evidence Layers](./04-ic-process-monitoring-and-failure-analysis/01-process-flow-and-evidence-layers.md)
- [Electrical Anomalies and Process Hypotheses](./04-ic-process-monitoring-and-failure-analysis/03-electrical-anomalies-and-process-hypotheses.md)
- [Emission Microscopy and Electrical Localization](./05-failure-localization-and-material-characterization/02-emission-microscopy-and-electrical-localization.md)
- [Reading SEM and EDS Signals](./05-failure-localization-and-material-characterization/03-electron-beam-signals-sem-and-eds.md)
- [FIB Cross-Sections, TEM Preparation, and Voltage Contrast](./05-failure-localization-and-material-characterization/04-fib-tem-preparation-and-voltage-contrast.md)
