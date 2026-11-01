# Screencast Video Recording Script (IITM BS MLOps Rubric A–J)
## Week 4: Integrating Continuous Integration (CI) into the IRIS Pipeline

* **Student Name:** Nitin Chauhan  
* **Roll Number:** `22f2001251`  
* **Email:** `22f2001251@ds.study.iitm.ac.in`  
* **Course:** Machine Learning Operations (MLOps) — IIT Madras BS Degree  
* **Assignment:** Week 4 — Integrating CI into the IRIS Pipeline  
* **Repository:** `https://github.com/IITM-22f2001251/22f2001251_MLOPS_WEEKLY_ASSIGNMENT`  
* **Target Duration:** 3 to 5 minutes  
* **Submission Screencast File Name:** `22f2001251Assignment4SEPT2026_MLOps.mp4`

---

## Rubric Breakdown Checklist (A through J)

- [x] **A. Explaining the Problem Statement**
- [x] **B. Explaining your approach to reach the objective**
- [x] **C. Explaining and demonstrating the configuration of cloud compute setup**
- [x] **D. Explaining Input files/data**
- [x] **E. Explaining and demonstrating sequence of actions performed**
- [x] **F. Exhaustive explanation of scripts/code and its objective**
- [x] **G. Errors encountered in the process and how they were overcome**
- [x] **H. Working demonstration of your pipeline (Live Demo on Vertex AI & GitHub Actions)**
- [x] **I. Explaining output files/data**
- [x] **J. Learnings from this Assignment**

---

## Detailed Word-by-Word Script with Visual Cues

### [0:00 - 0:30] A. Explaining the Problem Statement
* **🖥️ Screen Action:** Display the GitHub repository homepage and README header showing student details: Nitin Chauhan (`22f2001251`), course name, and Week 4 assignment title.
* **🎙️ Spoken Dialogue:**
> "Hello everyone, my name is Nitin Chauhan, Roll Number 22f2001251, enrolled in the IIT Madras BS Degree in Data Science and Applications. This is my video screencast for the Week 4 MLOps graded assignment: Integrating Continuous Integration into the IRIS Pipeline.  
>  
> In Weeks 1 to 3, we built an IRIS classification pipeline on Vertex AI, added DVC for data and model versioning, and integrated Feast for feature serving. However, every time code was pushed, there was no automated verification to confirm whether the pipeline still adhered to data invariants or produced acceptable accuracy. Continuous Integration (CI) closes this critical operational gap by automatically pulling versioned data and models via DVC, executing validation and evaluation tests on every commit, and publishing diagnostic reports directly to pull requests before merging into main."

---

### [0:30 - 0:55] B. Explaining Your Approach to Reach the Objective
* **🖥️ Screen Action:** Show the architecture flowchart in `README.md` or a split screen between GitHub Actions and Vertex AI Workbench.
* **🎙️ Spoken Dialogue:**
> "My approach establishes an automated quality gate architecture using GitHub Actions, DVC, Pytest, and Continuous Machine Learning (CML):  
> 1. **Trigger on Every Push & PR:** The workflow triggers on all commits and pull requests across branches.  
> 2. **DVC Artifact Pull:** The runner authenticates and executes `dvc pull` to fetch versioned data (`data/iris.csv`) and model binaries (`models/model.joblib`) from our GCS remote.  
> 3. **Pytest Quality Gates:** Runs 17 unit tests across two suites—validating data schema integrity and asserting that model metrics meet or exceed the 90% threshold.  
> 4. **CML Feedback Loop:** Automatically publishes an interactive evaluation report and confusion matrix as a comment on the Pull Request.  
> 5. **Quality-Gated Merge:** Code is only merged into `main` after all quality gates pass."

---

### [0:55 - 1:20] C. Configuration of Cloud Compute Setup
* **🖥️ Screen Action:** Show Google Cloud Console Vertex AI Workbench instance details and the GitHub Actions workflow environment.
* **🎙️ Spoken Dialogue:**
> "All operations and pipeline tests were configured and validated in the cloud:  
> - **Compute Environment:** Google Cloud Vertex AI user-managed Workbench instance `instance-20261011-192557` in zone `us-central1-a` (Project `88792490605` / `project-97a8c7d5-b469-40bc-80c`) running Debian with Python 3.11.  
> - **Cloud Storage:** Bucket `gs://mlops-assignment-iitm` hosting our DVC remote store at `week_2/dvc_store`.  
> - **CI Runner:** GitHub Actions `ubuntu-latest` running Python 3.11 with `pytest`, `dvc`, `dvc-gs`, and `setup-cml@v2`.  
> - **Permissions:** Granted Workload Identity Federation authentication and `pull-requests: write` permissions for automated commenting."

---

### [1:20 - 1:45] D. Explaining Input Files & Data
* **🖥️ Screen Action:** Show `data/iris.csv.dvc` and `models/model.joblib.dvc` in the terminal or editor.
* **🎙️ Spoken Dialogue:**
> "Our input assets are version-controlled using DVC pointers rather than committing heavy binaries into Git:  
> - **Dataset (`data/iris.csv`):** 150 biological observations containing 4 continuous morphological features (`sepal_length`, `sepal_width`, `petal_length`, `petal_width`) and target `species` (Setosa, Versicolor, Virginica). It is tracked by `data/iris.csv.dvc` with MD5 hash `843050135e5a83df3b24e72160180706`.  
> - **Model Binary (`models/model.joblib`):** Serialized Decision Tree classifier tracked by `models/model.joblib.dvc` with MD5 hash `01b7a2ebc28e50874649bc9d92f0001d`.  
>  
> Both files reside in GCS remote storage and are materialized on-demand using `dvc pull`."

---

### [1:45 - 2:15] E. Sequence of Actions Performed
* **🖥️ Screen Action:** Show the repository git log (`git log --oneline -n 6`).
* **🎙️ Spoken Dialogue:**
> "The sequence of actions performed was:  
> 1. Created `tests/test_data_validation.py` implementing 8 data invariant tests.  
> 2. Created `tests/test_model_evaluation.py` implementing 9 model quality gate assertions with a 90% benchmark.  
> 3. Configured `.github/workflows/ci.yml` defining the CI pipeline with DVC pull, Pytest, and CML reporting.  
> 4. Enabled unrestricted workflow triggers for every push and pull request across all branches.  
> 5. Created `generate_cml_report.py` to evaluate predictions and build `cml_report.md`.  
> 6. Opened Pull Request #3 from `week_4` to `main`, verified the automated CI run and CML comment, and completed the merge."

---

### [2:15 - 2:45] F. Exhaustive Explanation of Scripts & Code
* **🖥️ Screen Action:** Open `tests/test_data_validation.py` and `tests/test_model_evaluation.py`.
* **🎙️ Spoken Dialogue:**
> "Looking at the implementation code:  
> - **`tests/test_data_validation.py` (`TestIrisDataSchemaAndIntegrity`):** Validates dataset presence, non-zero size, required columns, zero missing values, float datatypes, positive measurements (>0.0 cm), canonical botanical ranges (e.g., sepal length 3.0 to 10.0 cm), and class representation.  
> - **`tests/test_model_evaluation.py` (`TestIrisModelQualityGates`):** Asserts model deserialization, batch inference alignment, and enforces that Accuracy, Macro Precision, Recall, and F1-Score all exceed the 90% operational benchmark. It also includes `test_regression_guard_catches_degraded_model` verifying that a subpar dummy classifier deliberately fails the test suite.  
> - **`generate_cml_report.py`:** Generates publication-ready markdown with per-class metrics and confusion matrix."

---

### [2:45 - 3:15] G. Errors Encountered in the Process & How They Were Overcome
* **🖥️ Screen Action:** Focus on `.github/workflows/ci.yml` and `tests/conftest.py`.
* **🎙️ Spoken Dialogue:**
> "During the assignment, we resolved two real-world engineering challenges:  
> 1. **DVC Remote Access in Headless CI Runners:** GitHub Actions runners lack interactive Google Cloud login credentials. We solved this by implementing both Workload Identity Federation authentication and an intelligent fallback via `sync_cache.py`, ensuring reliable artifact materialization across all environments.  
> 2. **CSV Header Encoding Variations:** Byte Order Marks (BOM) in CSV files can corrupt column headers. In `tests/conftest.py`, we sanitized headers by stripping `\\ufeff` characters to ensure consistent column resolution."

---

### [3:15 - 4:15] H. Working Demonstration of Pipeline (CORE LIVE DEMO)
* **🖥️ Screen Action 1 (Vertex AI Terminal):** 
  Switch to the Vertex AI Workbench terminal and run:
  ```bash
  cd ~/22f2001251_MLOPS_WEEKLY_ASSIGNMENT
  git branch
  ls -lh data/iris.csv models/model.joblib
  python -m pytest tests/ -v
  ```
* **🎙️ Spoken Dialogue:**
> "Now let's demonstrate the live pipeline. First, here in our Vertex AI Workbench terminal:  
> We confirm we are on branch `week_4`, and both `data/iris.csv` and `models/model.joblib` are materialized.  
> Now let's execute our automated Pytest suite:"  
*(Show terminal running tests)*  
> "Notice: All 17 unit tests execute in just under 4 seconds—8 data validation tests and 9 model quality tests—all passing with green status!  
> Next, let's run `python generate_cml_report.py`:"  
*(Run `python generate_cml_report.py` and show the formatted metrics table)*  
> "Our Decision Tree achieves **97.33% Accuracy**, **0.9738 Precision**, **0.9733 Recall**, and **0.9733 F1**—comfortably exceeding our 90% operational quality gate."

* **🖥️ Screen Action 2 (GitHub Actions & PR #3):**
  Switch browser tab to GitHub repository:
  1. Open **Actions** tab -> Show completed runs for PR #3 and main (both showing green checkmarks ✅).
  2. Open **Pull requests** > PR #3 (Merged) -> Show conversation comment by `github-actions[bot]`.
* **🎙️ Spoken Dialogue:**
> "Now let's view the automated execution on GitHub Actions:  
> Here in the Actions tab, you can see Workflow Run #41343506818 triggered automatically by Pull Request #3 from `week_4` to `main`. Every step succeeded: setting up Python 3.11, pulling DVC artifacts, running pytest, and posting the CML report.  
>  
> Switching to Pull Request #3 conversation: Here is the automated comment posted by `github-actions[bot]`. It displays our Quality Gate Performance Matrix, granular per-class metrics, and confusion matrix.  
>  
> With all 17 tests passed and quality gates confirmed, Pull Request #3 was cleanly merged into `main`!"

---

### [4:15 - 4:40] I. Explaining Output Files & Data
* **🖥️ Screen Action:** Show `cml_report.md` and `outputs/pipeline_run_log.txt` in the repository.
* **🎙️ Spoken Dialogue:**
> "The pipeline produces three essential outputs:  
> 1. **`cml_report.md`:** A persistent diagnostic markdown record tracking benchmark scores and confusion matrix.  
> 2. **Pull Request Comment:** A permanent, auditable evaluation report inside GitHub PR #3.  
> 3. **Interactive Walkthrough Notebook:** `22f2001251Assignment4SEPT2026_MLOps.ipynb` enabling interactive cell-by-cell execution in Vertex AI."

---

### [4:40 - 5:00] J. Learnings from this Assignment
* **🖥️ Screen Action:** Return to repository main page showing clean status and passing badges.
* **🎙️ Spoken Dialogue:**
> "To conclude, the key takeaways from Week 4 are:  
> 1. How Continuous Integration enforces quality gates to prevent silent model degradation before merging code.  
> 2. How DVC and GitHub Actions seamlessly pull versioned cloud artifacts into automated test runners.  
> 3. How CML bridges machine learning evaluation directly into developer pull request discussions.  
>  
> Thank you!"

---

## Quick Reference for Recording
* **File Name to Save Video:** `22f2001251Assignment4SEPT2026_MLOps.mp4`
* **Target Duration:** 3:30 to 4:45 minutes
* **Collaborator:** `IITMBSMLOps` (`da5014_1@study.iitm.ac.in`)
* **Repository Link:** `https://github.com/IITM-22f2001251/22f2001251_MLOPS_WEEKLY_ASSIGNMENT`
