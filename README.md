# Healthcare Education: Program Completions

This project uses NCES IPEDS to explore qualifications awarded in nursing and related healthcare programs during July 2022–June 2023. The notebook contains ingestion, two cleaning functions, grouped analysis, and three visualizations. The academic report, module_summary.pdf, includes my research-based motivation and reflection.

[GitHub repository](https://github.com/brandirobinson0581-cpu/ai-programming-foundations-project)

## Data

- [IPEDS download portal](https://nces.ed.gov/ipeds/use-the-data/download-access-database)
- [2023 completions CSV archive](https://nces.ed.gov/ipeds/datacenter/data/C2023_A.zip): `C2023_a_RV.csv`, final/revised release.
- [2023 institutional directory](https://nces.ed.gov/ipeds/datacenter/data/HD2023.zip): `HD2023.csv`.
- [Completions dictionary](https://nces.ed.gov/ipeds/datacenter/data/C2023_A_Dict.zip).

The local `healthcare_completions_2023.csv` selects CIP codes beginning with `51.` and retains institution ID, program code, major number, award level, total/men/women award counts, and their reporting flags. Official program and award labels and institution name, state, control, and sector are joined to those records. Second majors remain in the extract for explicit selection in the notebook. Counts are awards, not unique people; blank values have not been replaced with zeros. The extract excludes other CIP families, including some potentially health-adjacent programs.

## Responsible Practice: Bias and Data Quality

The geographical filter excludes territories and freely associated states. That makes the scope consistent but means the findings cannot represent every location in the source. Restricting the analysis to CIP series 51 also excludes health-adjacent programs classified elsewhere. Dropping zero-award programs would raise average awards per record; treating missing counts as zero in a future release could lower totals. Those transformations are not performed here.

All total-award flags in this extract are R (reported), but reporting status does not eliminate possible reporting errors. Award counts do not identify unique graduates, licensure success, employment, or learning outcomes. A single reporting year cannot establish trends or causal effects. A next analysis could add population denominators, examine territories separately, and compare multiple years using consistent program definitions.

## Future Integration Reflections

### Machine learning

A prediction task would need a defined outcome and an appropriate baseline. Predicting future award counts would require multiple years, a time-based holdout, and preprocessing fitted only on training data. The current one-year dataset supports description, not claims about future performance or student learning.

### Neural networks

Categorical fields would need encoding, numeric inputs would need appropriate scaling, and the data would need conversion to tensors. Those transformations would be fitted on training data and then applied to validation and test data. A neural network would need to outperform simpler methods to justify its added complexity; this project does not establish that one is needed.

### Agentic automation

An agent could check for a new IPEDS release, validate its columns, run the approved cleaning functions, and flag changes in totals. Human review would still be needed for changes in definitions, exclusions, and interpretation. Automation should not turn completion counts into unsupported claims about learning quality or readiness for clinical practice.

These reflections are also retained in `module_summary.pdf`.

## Run

Use Python 3.12 and a virtual environment. Install the captured dependencies:

```sh
python -m pip install -r requirements.txt
```

Open `data_workflow.ipynb` in a Jupyter-compatible editor, choose that environment as the kernel, and run all cells with the project directory as the working directory. Keep the CSV beside the notebook. The environment snapshot is generated with `python -m pip freeze > requirements.txt`.
