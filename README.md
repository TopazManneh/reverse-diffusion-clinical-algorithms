# UK Clinical Algorithms Audit: Automated Extraction and ONS Classification

This repository contains the Python scripts and extracted datasets auditing algorithmic adjustments, physiological reference ranges, and hardware disparities across UK clinical guidance.

## Datasets

* `uk_clinical_algorithms_audit.csv`: Compiled audit covering 16 active and baseline clinical algorithms across NICE, the BNF, ARTP/BTS, and the MHRA.
* `historical_removals_audit.csv`: Target dataset recording 4 confirmed historical de-adoption and deprecation events across the NICE CG and NG guidance series.

## Extraction and Classification Pipeline

The Python pipeline processes clinical text using regular expressions and parsing logic (`requests`, `BeautifulSoup`, `pandas`):

1. **Dual Regex Triggers:** Flags text blocks that simultaneously match clinical measurement language and demographic indicators.
2. **Harmonised ONS Classification:** Maps text directly to official UK Office for National Statistics (ONS) ethnic group taxonomy categories:
   * *Asian / Asian British* (e.g. Indian, Pakistani, Bangladeshi, Chinese, South Asian)
   * *Black / African / Caribbean / Black British* (e.g. African, Caribbean, African-Caribbean)
   * *Mixed / Multiple ethnic groups* (e.g. White and Black Caribbean, White and Asian)
   * *White* (e.g. British, Irish, White European)
   * *Other ethnic group* (e.g. Arab, Middle Eastern)
   * *Broad Demographic / Optical Classification* (e.g. minority ethnic, skin tone, dark-skinned, pigmentation, melanin)
3. **Categorisation of Operational Action:**
   * Risk Calculators and Prognostic Models (threshold adjustments, scoring tools)
   * Medications: Initiation and Monitoring (step-1 monotherapy, starter doses, pharmacogenetics)
   * Laboratory Tests and Biological Thresholds (reference intervals, equations, multipliers)
   * Medical Devices and Differential Performance (optical sensors, pulse oximetry)

## Historical De-adoption Auditing

The sweep checks historical revision logs (`/history`) and guideline chapters across 191 legacy Clinical Guidelines (`CG1` to `CG191`) for retirement verbs (`removed`, `deprecated`, `abandoned`, `discontinued`, `race-neutral`):

* **NICE NG203 (superseding CG182/CG73):** Removal of the 1.159 ethnicity multiplier for eGFR serum creatinine estimation.
* **ARTP / BTS Position Directive:** Replacement of the 10 to 15 percent lower lung function expectation for Black patients with race-neutral GLI 2022 equations.
* **NICE CG138 / CG55:** Discontinuation of radiographic pelvimetry and racial pelvic typing in labour.
* **NICE NG238 (superseding CG181):** Removal of automated blank-field risk calculation guidance in QRISK3.
