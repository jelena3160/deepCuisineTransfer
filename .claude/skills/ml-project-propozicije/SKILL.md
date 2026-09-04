---
name: ml-project-propozicije
description: Rules and requirements for creating and defending Machine Learning course projects. Use this skill whenever the user is working on, planning, structuring, reviewing, or preparing the defense of an ML/data science course project — e.g. when asking for help with a README file, organizing Jupyter notebooks, splitting code into scripts, saving trained models, evaluation (train/validation/test split), comparing models, or preparing a defense presentation. Also trigger when the user asks whether their project "meets the requirements", wants to check an existing project's compliance, or wants a checklist before submission/defense. Also activate on terms like "project defense", "demo application", "project propositions/requirements", or when the user uploads/describes a project structure that needs checking.
---

# Machine Learning Project Requirements (Creation & Defense)

This skill captures the course rules that every ML project (team or individual) must satisfy. Use it to (a) help plan/structure a new project, (b) audit an existing project against the checklist and flag gaps, or (c) help prepare the defense.

When reviewing an existing project, go through it file by file (README, notebooks, code, saved models, requirements) and explicitly mark each item below as ✅ met, ⚠️ partially met, or ❌ missing — don't just give a general impression that it looks fine.

## 1. Project Creation Checklist

### README.md (required)
- [ ] Project description (the problem being solved)
- [ ] Description of the dataset used
- [ ] References/literature used
- [ ] Names of all team members
- Especially important for self-proposed projects (not from the offered list) — the reviewer has no prior context, so the README must be self-sufficient for understanding the project.

### Jupyter Notebook Organization
- [ ] Notebooks are properly named with numeric prefixes (01, 02, 03...) indicating the order in which the project should be reviewed
- [ ] If the project uses Python scripts (.py) for the core logic, there must be a **final demo notebook** that showcases the functionality end-to-end

### Code Quality
- [ ] Code is decently commented
- [ ] There are instructions/comments that follow the flow of the project (a reader should be able to follow the logic without outside help)
- [ ] Debug/test print statements are commented out or redirected to log files — a notebook should not be long and cluttered with leftover debugging output

### Data Analysis
- [ ] Basic analysis of the dataset's structure (column types, size, missing values, etc.)
- [ ] Analysis of class/data (im)balance
- [ ] Highlighting interesting properties/patterns found in the data

### Model Evaluation and Results
- [ ] A clear **train / validation / test** split, correctly implemented — mistakes here are strictly penalized (e.g. data leakage, using the test set to tune hyperparameters, missing a separate validation set)
- [ ] Model results clearly presented (confusion matrices, relevant metrics — accuracy, F1, precision/recall, RMSE, etc., depending on the task)
- [ ] If multiple models are compared: a graphical comparison (e.g. a bar chart) plus a clear conclusion about which model performs better and why

### Saving Artifacts
- [ ] Trained models, scalers, vectorizers, etc. are saved (serialized, e.g. pickle/joblib/torch.save)
- [ ] If the files are too large for GitHub: follow the guidelines for large files (e.g. Git LFS) or provide a link to an external repository (Google Drive, OneDrive, WeTransfer, etc.)

### Environment
- [ ] A listing of required packages (e.g. requirements.txt, environment.yml, or clearly stated in the README)
- [ ] Setup instructions so someone else can test the project from scratch

### Team Work (if applicable)
- [ ] Even distribution of work among team members
- [ ] Commit history reflects individual contributions (not everything committed by one person, or in a single "bulk" commit at the end)
- Note: uneven engagement leads to scaled-down points per member, so actively check for this when helping plan a team's workflow (e.g. suggest each member works on their own branch/notebook and commits their part regularly).

## 2. Project Defense

- Defense dates are announced on the course announcements page.
- For the defense, you need to prepare:
  - a short **presentation** (PDF or Jupyter format)
  - a **demo application**, if the project includes such a component
- The presentation content should cover:
  - the problem addressed
  - the models and datasets used
  - the technologies and literature used
  - (optional, but nice to have) challenges encountered, unsuccessful attempts, interesting findings
- Time budget: **~10 minutes** for the presentation + **~5 minutes** for questions. When helping shape presentation content, keep this budget in mind — it's better to cut less important content than to run over time.
- For team projects, individual contributions are also tracked during the defense (see the commit-history point above) — it's good if every team member can explain their part.

## How to Use This Skill in Practice

- **When planning a new project**: propose a folder/notebook structure aligned with the checklist above before any code is written (e.g. `01_eda.ipynb`, `02_preprocessing.ipynb`, `03_modeling.ipynb`, `04_demo.ipynb`, `README.md`, `requirements.txt`, `models/`).
- **When reviewing an existing project**: go through the checklist item by item and give concrete, specifically located feedback (which file, what's missing).
- **When preparing for the defense**: help fit the content into the 10-minute budget while covering all required elements (problem, models, data, technologies, literature).
- The strictest item to emphasize whenever evaluation comes up: a correct train/validation/test split — this is explicitly called out as something that is strictly penalized if done incorrectly.
