# Operant Reward-Seeking Task for Mice
A Standardized Operant Paradigm for Assessing Motivation and Reward-Seeking Behavior in Mice 

<img width="1000" height="600" alt="graphical-abstract" src="https://github.com/user-attachments/assets/8c02fdeb-e109-476f-bc83-2ea9d10cc5b5" />

> ⚠️ If you use the protocol, MED-PC programs, behavioral analysis workflows, figures, or associated code contained in this repository, please cite the associated publication and repository (see Citation section below).

---

## Overview

This repository contains all experimental resources, control code, and analysis pipelines required to implement a standardized operant food-seeking paradigm in mice, designed for the quantitative assessment of motivational drive and reward-seeking behavior. The paradigm uses a two-port operant chamber in which animals learn an action-reward contingency. Responses at the active nose-poke port result in delivery of a palatable food reward, whereas responses at the inactive port have no programmed consequence.

The task is designed to:

- Assess acquisition of an action-reward contingency.
- Quantify reward-seeking behavior in the form of food-seeking behavior.
- Measure behavioral performance under increasing response demands (ie, increasing FR schedule).
- Assess behavioral flexibility using reversal learning (see Experimental Workflow in `FIGURES/`).
- Enable integration with fiber photometry recordings (see `MPC-CODE/FIBER/` and Experimental Workflow in `FIGURES/`).
- Support studies of neuropsychiatric and neurological disease models.

---

## Experimental Workflow Overview

### Behavioral paradigm

1. Establish baseline body weight.
2. Implement food restriction (85–90% free-feeding body weight).
3. Train mice under a Fixed Ratio 1 (FR1) schedule.
4. Increase response requirements using FR4 and FR8 schedules.
5. Optionally perform reversal learning by reversing active and inactive nose-poke ports (see Experimental Workflow in `FIGURES/`).

### Optional fiber photometry integration

1. Viral injection and optical fiber implantation.
2. Allow 3–4 weeks for viral expression.
3. Habituate mice to patch-cord connection.
4. Verify fluorescence signal quality.
5. Record neural activity during operant sessions.
6. Align behavioral events to neural activity using TTL synchronization.

---

## Behavioral Measures & MED-PC Variables

The paradigm records granular array data across session-level totals, time-stamped trial arrays, and computed performance indices (see MPC-CODE for more). Fiber photometry can be combined with the behavioral task to align real-time neural dynamics with discrete operant events.

### Task Acquisition & Discrimination

- **Food-related Responses (Active):** `W(0)` — Total responses at the active/reinforced port.
- **NoFood-related Responses (Inactive):** `W(1)` — Total responses at the inactive/non-reinforced port.
- **Percentage Food-related Responses:** `W(3)` — Percentage of active responses relative to total responses.
- **Percentage NoFood-related Responses:** `W(4)` — Percentage of inactive responses relative to total responses.
- **Preference Index (PI):** `W(5)` — Normalized discrimination index calculated as $(W(0) - W(1)) / W(2)$.
- **Total Task Responses:** `W(2)` — Combined active and inactive responses $(W(0) + W(1))$.
- **Total Food-related Nose-Pokes (NPs):** `F(1)` — Differentt from `W(0)` when FR schedule changes.
- **Total (Pellet) Rewards:** `F(2)` — Total food pellet deliveries earned.

### Response Dynamics & Temporal Profiling

- **Trial-by-Trial Event Array:** `D(J)` — Trial number, `D(J+1)` — Food-related response, `D(J+2)` — NoFood-related response, and within-session response timestamps `D(J+5)` for Food- and  `D(J+6)` for NoFood-related response.
- **Food-related Response Latencies:** `D(J+3)` — Trial active response latency, `W(6)` — Average active response latency.
- **NoFood-related Response Latencies:** `D(J+4)` — Trial inactive response latency, `W(7)` — Average inactive response latency.
- **Session Duration:** `S` — Total elapsed session time.

### Exploratory & Magazine Behavior

- **Total Head Entries:** `F(0)` — Total infrared beam breaks inside the food magazine.
- **Food-Magazine Entries:** Timestamped via `D(J+7)` (fiber photometry only).

---

## Repository Structure

``text
operant-reward-seeking/
│
├── README.md
├── LICENSE
├── CITATION.cff
│
├── MPC-CODE/
│   ├── FIBER/
│   ├── REWARD-SEEKING_FR1_LEFT.mpc
│   ├── REWARD-SEEKING_FR1_LEFT.mpc
│   ├── REWARD-SEEKING_FR4_LEFT.mpc
│   ├── REWARD-SEEKING_FR1_RIGHT.mpc
│   └── ...
│
├── MED-PC_to_EXCEL_TOOL/
│   ├── Session_transfer_code.MRP
│   ├── Session_transfer_image.png
│   ├── Trial-by-trial_transfer_code.MTP
│   └── Trial-by-trial_transfer_image.png
│
├── FIGURES/
│   └── Experimental_Workflow.png
│
├── RESULTS/
│   ├── MED-PC_Output-file.txt
│   ├── Session_Excel_results.png
│   └── Trial-by-trial_Excel_results.png

```

---

## MED-PC Programs

The repository includes behavioral-control programs (w/ or w/o fiber photometry) for:

- FR1 schedules 
- FR4 schedules
- FR8 schedules

Programs are provided for both:

- Left-active port configurations (ie, Food-related responses are on the Left nose-poke)
- Right-active port configurations (ie, Food-related responses are on the Right nose-poke)

Fiber photometry-compatible versions include TTL synchronization signals for acquisition triggering.

---

## Data Analysis & Processing Workflows

The images included in `MED-PC_to_EXCEL_TOOL/` show how to automate the extraction and processing of raw MED-PC data arrays into structured tabular outputs for statistical analysis.

### Behavioral Data Pipeline
- **Session-Level Metrics:** Automated calculation of total responses, reward delivery, and Preference Index.
- **Discrimination Analysis:** Quantification of active vs. inactive response ratios.
- **Temporal & Response Dynamics:** Extraction of trial-by-trial latencies and within-session response distribution.
- **Visualizations:** Generation of cumulative response curves, within-session raster plots, and longitudinal acquisition curves across FR/PR sessions.
- **Group Comparisons:** Structuring of multi-subject datasets for downstream statistical software (e.g., GraphPad Prism, R, Python).

---

## Translational & Research Applications

This standardized operant framework might also be suitable for neuroscientists investigating circuit-level mechanisms of motivation, reward processing, and executive function.

### Disease Models & Constructs
- **Frontotemporal Dementia (FTD) & Neurodegenerative Disorders:** Assessing apathy, reward devaluation, and loss of motivational drive.
- **Psychiatric & Mood Disorders:** Quantifying anhedonia and effort-based decision-making.
- **Neurodevelopmental Conditions:** Evaluating behavioral flexibility and perseverative responding during reversal learning.

### Circuit Neuroscience
- **In Vivo Photometry & Electrophysiology:** Real-time alignment of cell-type-specific neural activity with reward-seeking events via TTL synchronization.
- **Pharmacological & Optogenetic Manipulations:** Evaluating baseline vs. post-manipulation changes in effort exertion and task acquisition.

---

## Citation

If you use this repository, MED-PC procedures, or data extraction scripts, please cite both the software repository and the associated publication.

### Software Repository Citation
La Greca, F. (2026). operant-reward-seeking: A Standardized Operant Paradigm for Assessing Motivation and Reward-Seeking Behavior in Mice (Version 1.0.0). GitHub. https://github.com/filos93/operant-reward-seeking

### Associated Publication
Italia M., Salvadè M., La Greca F., Gardoni F., Scheggia D.. (2026). [A Standardized Operant Paradigm for Assessing Motivation and Reward-Seeking Behavior in Mice]. *[Jove]*, [Volume]([Issue]), [Pages]. https://doi.org/[DOI]

---

## License

This repository is released under the MIT License.

See the LICENSE file for details.

---

## Acknowledgements

This repository was developed to support standardized assessment of reward-seeking behavior and integration of behavioral and neural measurements in preclinical neuroscience research.

---

## Contact & Support

### Repository Maintainer
**Filippo La Greca**  
Department of Pharmacological and Biomolecular Sciences (DiSFeB)  
University of Milan  
*For questions regarding the code, MED-PC scripts, or converter tools, please open a GitHub Issue or contact the maintainer directly.*

### Corresponding Author / Principal Investigator
**Maria Italia**  
Department of Pharmacological and Biomolecular Sciences (DiSFeB)  
University of Milan  
*For scientific inquiries regarding the study or experimental design.*
