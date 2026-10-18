# Screencast Video Recording Script (IITM BS MLOps Rubric A–J)

**Student Name:** Nitin Chauhan  
**Roll Number:** 22f2001251  
**Course:** Machine Learning Operations (MLOps) — IIT Madras BS Degree  
**Assignment:** Week 2 — Integrating DVC into the IRIS Pipeline  
**Target Duration:** 3 to 5 minutes  

---

## Rubric Breakdown Checklist (A through J)

- [x] **A. Explaining the Problem Statement**
- [x] **B. Explaining your approach to reach the objective**
- [x] **C. Explaining and demonstrating the configuration of cloud compute setup**
- [x] **D. Explaining Input files/data**
- [x] **E. Explaining and demonstrating sequence of actions performed**
- [x] **F. Exhaustive explanation of scripts/code and its objective**
- [x] **G. Errors encountered in the process and how they were overcome**
- [x] **H. Working demonstration of your pipeline in GCP Environment**
- [x] **I. Explaining output files/data**
- [x] **J. Learnings from this Assignment**

---

## Detailed Word-by-Word Script with Visual Cues

### [0:00 - 0:30] A. Explaining the Problem Statement
* **🖥️ Screen Action:** Show Vertex AI Workbench terminal and README.md.
* **🎙️ Spoken Dialogue:**
> "Hello everyone, my name is Nitin Chauhan, Roll Number 22f2001251. This is my screencast for the Week 2 MLOps graded assignment on integrating Data Version Control (DVC) into the IRIS machine learning pipeline.  
>  
> In Week 1, we saved data and models into Google Cloud Storage buckets organized by execution timestamps. While this keeps storage organized, it leaves a critical gap: **it does not tell us which exact version of the data produced which model, and it doesn't allow instant rollback.** Traditional Git is not built to track large datasets and binary models without bloating the repository. That is why DVC is essential: it extends Git to track lightweight pointer hashes while storing actual artifacts in cloud storage."

---

### [0:30 - 0:55] B. Explaining Your Approach to Reach the Objective
* **🖥️ Screen Action:** Display repository structure in terminal or README.
* **🎙️ Spoken Dialogue:**
> "My approach coordinates three decoupled components:  
> 1. **Git Repository:** Tracks source code, configuration files, and tiny `.dvc` pointer files that hold cryptographic hashes of data and model artifacts.  
> 2. **GCS Remote Storage:** A dedicated Google Cloud Storage bucket that holds the heavy datasets and trained models.  
> 3. **Local DVC Cache:** A content-addressable local store inside `.dvc/cache` that enables instant version switching via `dvc checkout` without redownloading files unnecessarily."

---

### [0:55 - 1:20] C. Configuration of Cloud Compute Setup
* **🖥️ Screen Action:** Show JupyterLab environment and terminal header.
* **🎙️ Spoken Dialogue:**
> "All operations and pipeline runs were executed directly within the Google Cloud Platform environment:  
> - **Compute Instance:** Google Cloud Vertex AI Workbench user-managed notebook instance `instance-20261011-192557` in zone `us-central1-a` running Debian 12 with Python 3.12.  
> - **Cloud Storage:** Bucket `gs://mlops-assignment-iitm` in region `us`.  
> - **DVC Remote:** Configured to `gs://mlops-assignment-iitm/week_2/dvc_store`.  
> - **Environment Packages:** Installed `dvc[gs]`, `google-cloud-storage`, `scikit-learn`, `pandas`, and `joblib`."

---

### [1:20 - 1:45] D. Explaining Input Files & Data
* **🖥️ Screen Action:** Run `head -n 5 data/v1/data.csv` or show dataset files.
* **🎙️ Spoken Dialogue:**
> "Our input data is the IRIS dataset, consisting of four numerical features (`sepal_length`, `sepal_width`, `petal_length`, `petal_width`) and the target `species` (Setosa, Versicolor, Virginica).  
>  
> To simulate realistic ML iterations:  
> - **Iteration 1 (`v1.0`):** Base dataset `data/v1/data.csv` containing **101 samples** (102 lines with header).  
> - **Iteration 2 (`v2.0` / Latest `week_2`):** Augmented dataset `data/raw/iris.csv` containing **150 samples** (151 lines with header)."

---

### [1:45 - 2:20] E. Sequence of Actions Performed
* **🖥️ Screen Action:** Run `git log --oneline -n 6` to show clean history.
* **🎙️ Spoken Dialogue:**
> "The sequence of actions performed was:  
> 1. Initialized DVC inside the Git repository using `dvc init` and committed `.dvc/` configurations.  
> 2. Configured the default remote storage using `dvc remote add -d gcs_remote gs://mlops-assignment-iitm/week_2/dvc_store`.  
> 3. Versioned Iteration 1 with 101 samples, trained Model v1, tracked both files using `dvc add`, uploaded them using `dvc push`, and tagged `v1.0` in Git.  
> 4. Expanded to Iteration 2 with 150 samples, retrained Model v2, updated DVC tracking, pushed new hashes, and tagged `v2.0`.  
> 5. Verified dynamic version rollback using `dvc checkout` and synchronized all code to GitHub and artifacts to GCS."

---

### [2:20 - 2:45] F. Exhaustive Explanation of Scripts & Code
* **🖥️ Screen Action:** Open or display `src/train.py` and `data/iris.csv.dvc`.
* **🎙️ Spoken Dialogue:**
> "Looking at the implementation code:  
> - **`src/train.py`:** Contains `run_local_training()`, which loads `data/iris.csv`, trains a `DecisionTreeClassifier` with `max_depth=3`, computes training accuracy, and exports the serialized model binary to `models/model.joblib`.  
> - **`data/iris.csv.dvc` & `models/model.joblib.dvc`:** These are lightweight YAML pointer files containing MD5 hashes and file sizes. By tracking these pointer files in Git instead of heavy data, Git remains fast and lightweight while maintaining a 100% reproducible link between code, data, and models."

---

### [2:45 - 3:15] G. Errors Encountered in the Process & How They Were Overcome
* **🖥️ Screen Action:** Focus on terminal.
* **🎙️ Spoken Dialogue:**
> "During the implementation, we encountered and successfully resolved two real-world challenges:  
> 1. **GCS Permission Denied (403 Forbidden):** The Compute Engine service account (`88792490605-compute@developer.gserviceaccount.com`) initially lacked access to the bucket `mlops-assignment-iitm`. We resolved this by granting the `Storage Admin` (`roles/storage.admin`) IAM role to the service account.  
> 2. **DVC Cache Missing Across Environments:** When cloning or switching between environments, local cache files were absent. We resolved this by synchronizing our DVC cache across tags so both `v1.0` and `v2.0` MD5 hashes exist locally and in cloud storage."

---

### [3:15 - 4:10] H. Working Demonstration of Pipeline in GCP Environment (CORE DEMO)
* **🖥️ Screen Action:** Run live commands sequentially in Vertex AI terminal.
* **🎙️ Spoken Dialogue:**
> "Now, let's demonstrate the live pipeline on Vertex AI.  
>  
> First, let's inspect the DVC remote configuration:"  
```bash
dvc remote list
```
> "It shows `gcs_remote` pointing to `gs://mlops-assignment-iitm/week_2/dvc_store` as default.  
>  
> Next, let's verify our current latest version on branch `week_2`:"  
```bash
wc -l data/iris.csv
```
> "It shows **151 lines** (150 data rows + 1 header).  
>  
> Now let's demonstrate version time-travel: we switch Git to `v1.0` and run `dvc checkout`:"  
```bash
git checkout v1.0
dvc checkout
wc -l data/iris.csv
```
> "Notice that `data/iris.csv` immediately reverted to **102 lines** (101 data rows), and `models/model.joblib` reverted to Model v1!  
>  
> Now let's return to the latest version on branch `week_2`:"  
```bash
git checkout week_2
dvc checkout
wc -l data/iris.csv
```
> "The dataset is instantly restored back to **151 lines** (150 samples).  
>  
> Finally, let's verify synchronization with remote storage:"  
```bash
dvc push
```
> "It confirms: `Everything is up to date`."

---

### [4:10 - 4:35] I. Explaining Output Files & Data
* **🖥️ Screen Action:** Switch to browser tabs for Google Cloud Storage and GitHub.
* **🎙️ Spoken Dialogue:**
> "Here in the Google Cloud Console under `gs://mlops-assignment-iitm/week_2/dvc_store/`, you can see the content-addressable hash folders storing both versions of our datasets and trained model binaries.  
>  
> On GitHub on branch `week_2`, we only commit the `.dvc` pointer files and pipeline scripts, keeping our Git repository fully reproducible and lean."

---

### [4:35 - 5:00] J. Learnings from this Assignment
* **🖥️ Screen Action:** Show terminal with clean `git status`.
* **🎙️ Spoken Dialogue:**
> "To conclude, the key learnings from this assignment are:  
> 1. How DVC seamlessly bridges Git with Google Cloud Storage for large ML assets.  
> 2. Full auditability and provenance: we can trace the exact dataset version that produced any trained model.  
> 3. Instant reproducibility across different team members and cloud environments without data loss.  
>  
> Thank you!"

---

## Submission Details Reminder
- **File Name:** `22f2001251_Assignment_2_SEPT_2026_MLOps.mp4`
- **GitHub Branch:** `week_2`
- **Collaborator:** `IITMBSMLOps` (`da5014_1@study.iitm.ac.in`)
