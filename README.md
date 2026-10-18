**Intelligent Timetable for University**
OffDayOpt — constraint-aware evolutionary optimisation for university timetabling
A complete Python/Jupyter research project aligned with CSCU9YE Artificial Intelligence Units 4 and 5. Every scheduling algorithm, exact model, analysis, visualisation, export and regression test is implemented inside the notebooks. No research package or project .py module needs to be imported.
The benchmark has 16 cohorts, 18 module codes, 50 cohort-module offerings and 150 one-hour meetings. It protects the supplied weekly-off rules and the 12:30–13:30 lunch break within a Monday–Saturday, 09:30–15:30 calendar.
Start
Create and activate a Python 3.11 or 3.12 environment, then run:
python -m pip install -r requirements.txt
python -m ipykernel install --user --name offdayopt --display-name "OffDayOpt"
python -m jupyterlab
Open notebooks/01_OffDayOpt_Complete_Project.ipynb, select the OffDayOpt kernel and Restart Kernel and Run All Cells. The quick profile runs three seeds per algorithm with 200 complete fitness evaluations per run. Each execution writes a fresh timestamped outputs/ directory. It never overwrites the manuscript snapshot.
Windows environment activation uses .venv\Scripts\activate; macOS/Linux uses source .venv/bin/activate if you created the environment with python -m venv .venv.
Notebooks
File	Purpose
01_OffDayOpt_Complete_Project.ipynb	Full configurable implementation, analysis, exact feasibility, experiments, cohort timetables, plots and adversarial tests
02_Manuscript_Reproduction.ipynb	Original study implementation, frozen result checks and optional 30-seed timed rerun


Notebook 01 runs random repair, static-penalty GA, feasibility-first GA without repair, Lamarckian-repair GA and Baldwinian-repair GA. Its new implementation adds fixed-evaluation budgets, shuffled run order, defensive validation and heterogeneous-room exact feasibility. These enhancements were not evaluated in the manuscript's original four-arm study.
Inputs and provenance
Edit data/instance.json, then rerun Notebook 01. Its complete fallback dataset is embedded in the notebook for standalone use. The JSON defines the calendar, cohorts, modules, lecturers, rooms and required events. Every event is one required one-hour meeting. Calendar restrictions, lecturer/room unavailability, room type and room capacity are hard requirements.
The supplied module mappings and weekly-off rules are retained. Contact hours, student counts, lecturer assignments and room inventory are synthetic assumptions. Every offering has three assumed hours: usually two lectures plus one lab; MATU9S1, MGTU7S1 and CSCU9Z7 use three lecture/tutorial/project-supervision meetings. Project independent study is excluded. All listed modules are scheduled, without inferring elective alternatives.
DS2A and DS2B inherit Tuesday/Friday off. CS3 and SE3SQA have user-approved provisional availability on all six days. SE3A/B/C and SE3SQA use the SE Year 3 module list; DS3A/B use the DS Year 3 list. CSCU9P5 and CSCU9E5 remain distinct codes despite their identical supplied title.
See [the dataset guide](docs/DATASET.md) for the schema and [the method guide](docs/METHODOLOGY.md) for fitness and experimental limits.
Recorded manuscript evidence
paper_results/ is a frozen copy of the original study inputs, all 120 stochastic outcomes, selected assignment, independent validation, figures and exact resource certificates. The original four arms ran 30 seeds for approximately one second per run. The selected schedule has H=0 and S=113. Repaired methods and random repair succeeded 30/30; the tested static penalty succeeded 1/30.
These are historical results for one constructed workload. New quick-profile results are computed afresh and are not expected to match. Timed reruns depend on hardware. The exact solver's objective is zero; it certifies feasibility, not optimal soft quality. Four lecture rooms and two labs were sufficient under the original assumptions, with corresponding witnesses stored in the snapshot.
Verification
The first notebook contains executable unittest regression and adversarial tests. To execute both notebooks with Jupyter and validate their file structure:
python tools/run_with_jupyter.py --timeout 900
A lightweight shared-namespace code-cell verifier is also provided:
python tools/verify_notebooks.py
The lightweight verifier captures stdout, test output and Matplotlib images into the notebooks. It verifies Python execution, not browser rendering or the Jupyter messaging protocol. GitHub Actions executes the real Jupyter path on Python 3.11 and 3.12 after the repository is hosted. See VERIFICATION.md for checks actually performed before delivery.
Research scope
The model does not include contiguous multi-hour labs, individual cross-cohort elective enrolments, room travel, lecturer rest-day policies, multiple lecturers per module or minimal-change reactive scheduling. Some are discussed as extensions, not implemented features. Repair can fail; infeasible candidates remain failures, and no invalid candidate is silently exported as a timetable. Do not infer institutional adoption from the constructed benchmark.
GitHub setup
The project is ready to upload as repository offdayopt. The GitHub account connection is required to create the hosted repository from the assistant. If creating it yourself, use a new private repository named offdayopt, without a generated README, then upload this folder's contents including notebooks, data, paper_results, docs, tools and .github.
Alternatively, with Git and an authenticated GitHub CLI already installed:
git init -b main
git add .
git commit -m "Add complete OffDayOpt Jupyter research project"
gh repo create offdayopt --private --source=. --remote=origin --push
Do not run the creation command if a repository already exists; use its existing remote. Replace any repository-specific citation metadata after hosting. No public repository URL or DOI has been assigned in this project.
