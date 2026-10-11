# 🎙️ Screencast Walkthrough & Viva Presentation Script
**Course:** Machine Learning Operations (MLOps) — Graded Assignment Week 1  
**Student:** Nitin Chauhan (`22f2001251`) | **Repository:** `IITM-22f2001251/22f2001251_MLOPS_WEEKLY_ASSIGNMENT` (branch: `week_1`)  
**Evaluator:** `IITMBSMLOps` (`da5014_1@study.iitm.ac.in`)  
**Reference Checklist:** [image copy 8.png](file:///home/nitin/Desktop/mlops%20assignment/Nitin%20Chauhan/images/image%20copy%208.png)

---

## Quick Reference Summary Table

| Checklist Item | What File & Lines to Show on Screen | What to Say (Spoken Script) |
| :--- | :--- | :--- |
| **A. Problem Statement** | [README.md](file:///home/nitin/Desktop/mlops%20assignment/Nitin%20Chauhan/22f2001251_MLOPS_WEEKLY_ASSIGNMENT/README.md#L9-L20) (Lines 9–20) | *"The objective is to build an end-to-end, reproducible MLOps pipeline on GCP for the Iris dataset—covering Vertex AI Workbench, GCS data & artifact tracking, decoupled training and inference, and multi-version evaluation."* |
| **B. Approach to Reach Objective** | [README.md](file:///home/nitin/Desktop/mlops%20assignment/Nitin%20Chauhan/22f2001251_MLOPS_WEEKLY_ASSIGNMENT/README.md#L24-L45) (Lines 24–45)<br>[run_pipeline.py](file:///home/nitin/Desktop/mlops%20assignment/Nitin%20Chauhan/22f2001251_MLOPS_WEEKLY_ASSIGNMENT/run_pipeline.py#L49-L87) (Lines 49–87) | *"Instead of a monolithic notebook, I used a modular architecture under `src/`. Training and inference are fully decoupled: `train.py` pushes model artifacts to GCS, and `inference.py` pulls them from GCS without shared local memory."* |
| **C. Cloud Compute Setup** | [config.py](file:///home/nitin/Desktop/mlops%20assignment/Nitin%20Chauhan/22f2001251_MLOPS_WEEKLY_ASSIGNMENT/config.py#L4-L16) (Lines 4–16)<br>[image copy.png](file:///home/nitin/Desktop/mlops%20assignment/Nitin%20Chauhan/images/image%20copy.png) & [image copy 3.png](file:///home/nitin/Desktop/mlops%20assignment/Nitin%20Chauhan/images/image%20copy%203.png) | *"I configured a Vertex AI Workbench instance `instance-20261011-192557` in `us-central1-a` (`e2-standard-4`, 4 vCPUs, 16 GB RAM, Debian 12, Python 3.12) and a GCS bucket `gs://week_1_artifacts` in `us-east1`."* |
| **D. Input Files / Data** | [data/raw/iris.csv](file:///home/nitin/Desktop/mlops%20assignment/Nitin%20Chauhan/22f2001251_MLOPS_WEEKLY_ASSIGNMENT/data/raw/iris.csv#L1-L10) (Lines 1–10)<br>[src/store_data.py](file:///home/nitin/Desktop/mlops%20assignment/Nitin%20Chauhan/22f2001251_MLOPS_WEEKLY_ASSIGNMENT/src/store_data.py#L53-L66) (Lines 53–66) | *"The raw dataset has 150 samples across 3 balanced species classes. We perform a stratified 70/30 split into 105 training samples and 45 evaluation samples, alongside version 1 (101 samples) and version 2 (49 samples)."* |
| **E. Sequence of Actions Performed** | [image copy 4.png](file:///home/nitin/Desktop/mlops%20assignment/Nitin%20Chauhan/images/image%20copy%204.png) (JupyterLab Terminal)<br>[README.md](file:///home/nitin/Desktop/mlops%20assignment/Nitin%20Chauhan/22f2001251_MLOPS_WEEKLY_ASSIGNMENT/README.md#L61-L107) (Lines 61–107 & 141–144) | *"Actions: provision GCP resources, launch JupyterLab terminal, clone private repository on `week_1` branch, add collaborator `IITMBSMLOps`, install dependencies, run pipeline, and verify GCS artifacts."* |
| **F. Explanation of Scripts & Code** | [src/store_data.py](file:///home/nitin/Desktop/mlops%20assignment/Nitin%20Chauhan/22f2001251_MLOPS_WEEKLY_ASSIGNMENT/src/store_data.py#L31-L83) (Lines 31–83)<br>[src/train.py](file:///home/nitin/Desktop/mlops%20assignment/Nitin%20Chauhan/22f2001251_MLOPS_WEEKLY_ASSIGNMENT/src/train.py#L77-L142) (Lines 77–142)<br>[src/inference.py](file:///home/nitin/Desktop/mlops%20assignment/Nitin%20Chauhan/22f2001251_MLOPS_WEEKLY_ASSIGNMENT/src/inference.py#L108-L158) (Lines 108–158)<br>[src/compare_versions.py](file:///home/nitin/Desktop/mlops%20assignment/Nitin%20Chauhan/22f2001251_MLOPS_WEEKLY_ASSIGNMENT/src/compare_versions.py#L77-L115) (Lines 77–115) | *"`store_data.py` splits & uploads data to GCS. `train.py` fetches data from GCS, fits the model, and uploads `model.joblib` & metrics. `inference.py` loads model & eval data from GCS to predict. `compare_versions.py` assesses v1 vs v2."* |
| **G. Errors Encountered & Solutions** | [src/store_data.py](file:///home/nitin/Desktop/mlops%20assignment/Nitin%20Chauhan/22f2001251_MLOPS_WEEKLY_ASSIGNMENT/src/store_data.py#L54-L55) (Lines 54–55)<br>[src/inference.py](file:///home/nitin/Desktop/mlops%20assignment/Nitin%20Chauhan/22f2001251_MLOPS_WEEKLY_ASSIGNMENT/src/inference.py#L36-L49) (Lines 36–49)<br>[run_pipeline.py](file:///home/nitin/Desktop/mlops%20assignment/Nitin%20Chauhan/22f2001251_MLOPS_WEEKLY_ASSIGNMENT/run_pipeline.py#L68-L70) (Lines 68–70) | *"1. Handled hidden UTF-8 BOM (`\ufeff`) header in CSV. 2. Eliminated train/infer in-memory coupling via GCS byte serialization. 3. Added 3-second sleep delay to avoid timestamp folder collisions in Task 5. 4. Ignored binaries in Git via `.gitignore`."* |
| **H. Working Pipeline Demonstration** | [outputs/pipeline_run_log.txt](file:///home/nitin/Desktop/mlops%20assignment/Nitin%20Chauhan/22f2001251_MLOPS_WEEKLY_ASSIGNMENT/outputs/pipeline_run_log.txt#L17-L34) (Lines 17–34)<br>[pipeline_notebook.ipynb](file:///home/nitin/Desktop/mlops%20assignment/Nitin%20Chauhan/22f2001251_MLOPS_WEEKLY_ASSIGNMENT/pipeline_notebook.ipynb) | *"Here is the executed pipeline: Run 1 completed at `2026-10-11T16-05-35` (Train: 98.10%, Eval: 93.33%). Run 2 completed at `2026-10-11T16-05-41` (Train: 98.10%, Eval: 93.33%), demonstrating consistent reproducibility across unique GCS folders."* |
| **I. Output Files / Data** | [README.md](file:///home/nitin/Desktop/mlops%20assignment/Nitin%20Chauhan/22f2001251_MLOPS_WEEKLY_ASSIGNMENT/README.md#L110-L137) (Lines 110–137)<br>[outputs/data_version_comparison_report.txt](file:///home/nitin/Desktop/mlops%20assignment/Nitin%20Chauhan/22f2001251_MLOPS_WEEKLY_ASSIGNMENT/outputs/data_version_comparison_report.txt#L1-L12) (Lines 1–12) | *"All artifacts are stored under `gs://week_1_artifacts/`: `data/` has the split datasets, and `artifacts/<TIMESTAMP>/` holds `model.joblib`, `train_metrics.json`, `predictions.csv`, and `eval_metrics.json`."* |
| **J. Learnings from Assignment** | [outputs/data_version_comparison_report.txt](file:///home/nitin/Desktop/mlops%20assignment/Nitin%20Chauhan/22f2001251_MLOPS_WEEKLY_ASSIGNMENT/outputs/data_version_comparison_report.txt#L6-L10) (Lines 6–10) | *"Key learnings: decoupled pipelines prevent leakage; GCS provides a persistent single source of truth; and smaller/skewed datasets cause severe overfitting (Version 2 got 100% train accuracy but eval dropped to 86.67%)."* |

---

## Detailed Step-by-Step Walkthrough

### **A. Explaining the Problem Statement**
* **On Screen:** Open [`README.md`](file:///home/nitin/Desktop/mlops%20assignment/Nitin%20Chauhan/22f2001251_MLOPS_WEEKLY_ASSIGNMENT/README.md#L9-L20) and highlight **Lines 9 to 20**.
* **Spoken Script:**
  > *"The objective of this assignment is to build a production-grade, reproducible MLOps pipeline on Google Cloud Platform for the Iris dataset. We set up Vertex AI Workbench and GCS, decoupled the training and inference pipelines, ensured multi-run tracking with timestamped artifacts, and evaluated performance across multiple data versions."*

---

### **B. Explaining Your Approach to Reach the Objective**
* **On Screen:** 
  1. Open [`README.md`](file:///home/nitin/Desktop/mlops%20assignment/Nitin%20Chauhan/22f2001251_MLOPS_WEEKLY_ASSIGNMENT/README.md#L24-L45) to highlight the repository layout (Lines 24–45).
  2. Open [`run_pipeline.py`](file:///home/nitin/Desktop/mlops%20assignment/Nitin%20Chauhan/22f2001251_MLOPS_WEEKLY_ASSIGNMENT/run_pipeline.py#L49-L87) to highlight the orchestration flow (Lines 49–87).
* **Spoken Script:**
  > *"Instead of a monolithic notebook, I adopted a modular architecture under `src/`. Training and inference are fully decoupled: `train.py` pushes the trained model to Cloud Storage, and `inference.py` pulls both the model and evaluation dataset dynamically from GCS. Everything is orchestrated end-to-end via `run_pipeline.py`."*

---

### **C. Configuration of Cloud Compute Setup**
* **On Screen:**
  1. Open [`config.py`](file:///home/nitin/Desktop/mlops%20assignment/Nitin%20Chauhan/22f2001251_MLOPS_WEEKLY_ASSIGNMENT/config.py#L4-L16) (Lines 4–16).
  2. Show screenshot [image copy.png](file:///home/nitin/Desktop/mlops%20assignment/Nitin%20Chauhan/images/image%20copy.png) for Vertex AI Workbench.
  3. Show screenshot [image copy 3.png](file:///home/nitin/Desktop/mlops%20assignment/Nitin%20Chauhan/images/image%20copy%203.png) for GCS bucket.
* **Spoken Script:**
  > *"I provisioned a Vertex AI Workbench instance named `instance-20261011-192557` in `us-central1-a` with an `e2-standard-4` machine type running Debian 12 and Python 3.12. For artifact and dataset storage, I created a Google Cloud Storage bucket named `gs://week_1_artifacts` located in `us-east1`."*

---

### **D. Explaining Input Files / Data**
* **On Screen:**
  1. Open [`data/raw/iris.csv`](file:///home/nitin/Desktop/mlops%20assignment/Nitin%20Chauhan/22f2001251_MLOPS_WEEKLY_ASSIGNMENT/data/raw/iris.csv#L1-L10) (Lines 1–10).
  2. Open [`src/store_data.py`](file:///home/nitin/Desktop/mlops%20assignment/Nitin%20Chauhan/22f2001251_MLOPS_WEEKLY_ASSIGNMENT/src/store_data.py#L53-L66) (Lines 53–66).
* **Spoken Script:**
  > *"Our primary input is the raw Iris dataset with 150 rows across 3 balanced species classes. In `store_data.py`, we perform a 70/30 stratified split resulting in 105 training samples and 45 evaluation samples, and also ingest versions `v1` with 101 rows and `v2` with 49 rows for drift analysis."*

---

### **E. Sequence of Actions Performed**
* **On Screen:**
  1. Show screenshot [image copy 4.png](file:///home/nitin/Desktop/mlops%20assignment/Nitin%20Chauhan/images/image%20copy%204.png) (JupyterLab Terminal).
  2. Open [`README.md`](file:///home/nitin/Desktop/mlops%20assignment/Nitin%20Chauhan/22f2001251_MLOPS_WEEKLY_ASSIGNMENT/README.md#L61-L107) (Lines 61–107 and 141–144).
* **Spoken Script:**
  > *"The sequence was: first, provision compute and storage on GCP; second, launch JupyterLab and open the terminal; third, clone our private Git repository on the `week_1` branch and invite `IITMBSMLOps` as collaborator; fourth, install requirements; and finally, trigger the pipeline."*

---

### **F. Exhaustive Explanation of Scripts & Code**
* **On Screen:**
  1. [`src/store_data.py`](file:///home/nitin/Desktop/mlops%20assignment/Nitin%20Chauhan/22f2001251_MLOPS_WEEKLY_ASSIGNMENT/src/store_data.py#L31-L83) (Lines 31–83) ➔ `prepare_and_store_data`
  2. [`src/train.py`](file:///home/nitin/Desktop/mlops%20assignment/Nitin%20Chauhan/22f2001251_MLOPS_WEEKLY_ASSIGNMENT/src/train.py#L77-L142) (Lines 77–142) ➔ `run_training`
  3. [`src/inference.py`](file:///home/nitin/Desktop/mlops%20assignment/Nitin%20Chauhan/22f2001251_MLOPS_WEEKLY_ASSIGNMENT/src/inference.py#L108-L158) (Lines 108–158) ➔ `run_inference`
  4. [`src/compare_versions.py`](file:///home/nitin/Desktop/mlops%20assignment/Nitin%20Chauhan/22f2001251_MLOPS_WEEKLY_ASSIGNMENT/src/compare_versions.py#L77-L115) (Lines 77–115) ➔ `compare_data_versions`
* **Spoken Script:**
  > *"`store_data.py` splits and uploads data directly to GCS. `train.py` fetches `train.csv` from GCS, fits the Decision Tree classifier, and saves `model.joblib` and metrics under a timestamped GCS folder. `inference.py` independently fetches the model and `eval.csv` to make predictions and upload metrics. `compare_versions.py` automates evaluating version 1 versus version 2."*

---

### **G. Errors Encountered & Solutions**
* **On Screen:**
  1. [`src/store_data.py`](file:///home/nitin/Desktop/mlops%20assignment/Nitin%20Chauhan/22f2001251_MLOPS_WEEKLY_ASSIGNMENT/src/store_data.py#L54-L55) (Lines 54–55): BOM character removal.
  2. [`src/inference.py`](file:///home/nitin/Desktop/mlops%20assignment/Nitin%20Chauhan/22f2001251_MLOPS_WEEKLY_ASSIGNMENT/src/inference.py#L36-L49) (Lines 36–49): GCS model loading.
  3. [`run_pipeline.py`](file:///home/nitin/Desktop/mlops%20assignment/Nitin%20Chauhan/22f2001251_MLOPS_WEEKLY_ASSIGNMENT/run_pipeline.py#L68-L70) (Lines 68–70): 3-second sleep delay.
  4. [`.gitignore`](file:///home/nitin/Desktop/mlops%20assignment/Nitin%20Chauhan/22f2001251_MLOPS_WEEKLY_ASSIGNMENT/.gitignore#L1-L10) (Lines 1–10): Excluded binary model files and video recordings.
* **Spoken Script:**
  > *"I encountered four key challenges: first, a UTF-8 BOM in the CSV header which I sanitized using `str.replace`; second, preventing in-memory coupling by loading the model purely from GCS bytes; third, adding a 3-second pause to prevent timestamp collisions across runs; and fourth, setting `.gitignore` to keep binaries out of the Git repo."*

---

### **H. Working Pipeline Demonstration**
* **On Screen:**
  1. Open [`outputs/pipeline_run_log.txt`](file:///home/nitin/Desktop/mlops%20assignment/Nitin%20Chauhan/22f2001251_MLOPS_WEEKLY_ASSIGNMENT/outputs/pipeline_run_log.txt#L17-L34) (Lines 17–34).
  2. Or show executed cells in [`pipeline_notebook.ipynb`](file:///home/nitin/Desktop/mlops%20assignment/Nitin%20Chauhan/22f2001251_MLOPS_WEEKLY_ASSIGNMENT/pipeline_notebook.ipynb).
* **Spoken Script:**
  > *"Here is the executed log showing both runs: Run 1 completed at timestamp `2026-10-11T16-05-35` with 98.10% training accuracy and 93.33% evaluation accuracy. Run 2 completed at `2026-10-11T16-05-41` with identical metrics, proving reproducibility across independent timestamped runs."*

---

### **I. Explaining Output Files / Data**
* **On Screen:**
  1. Open [`README.md`](file:///home/nitin/Desktop/mlops%20assignment/Nitin%20Chauhan/22f2001251_MLOPS_WEEKLY_ASSIGNMENT/README.md#L110-L137) (Lines 110–137).
  2. Open [`outputs/data_version_comparison_report.txt`](file:///home/nitin/Desktop/mlops%20assignment/Nitin%20Chauhan/22f2001251_MLOPS_WEEKLY_ASSIGNMENT/outputs/data_version_comparison_report.txt#L1-L12) (Lines 1–12).
* **Spoken Script:**
  > *"In GCS under `gs://week_1_artifacts/`, we have `data/` containing our split datasets, and `artifacts/` containing separate timestamped folders for each run with `model.joblib`, `predictions.csv`, `train_metrics.json`, and logs. We also have `data_version_comparison_report.txt` comparing versions 1 and 2."*

---

### **J. Key Learnings from this Assignment**
* **On Screen:** Open [`outputs/data_version_comparison_report.txt`](file:///home/nitin/Desktop/mlops%20assignment/Nitin%20Chauhan/22f2001251_MLOPS_WEEKLY_ASSIGNMENT/outputs/data_version_comparison_report.txt#L6-L10) (Lines 6–10).
* **Spoken Script:**
  > *"My key takeaways: First, decoupling train and inference stages guarantees clean deployment boundaries. Second, using GCS as the single source of truth provides cloud persistence. And third, from Task 6, we saw how smaller datasets like Version 2 cause severe overfitting—reaching 100% training accuracy but dropping evaluation accuracy from 96.77% down to 86.67%."*
