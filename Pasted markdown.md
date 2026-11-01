**# Screencast Video Recording Script (IITM BS MLOps Rubric A–J)**

**## Week 4: Integrating Continuous Integration (CI) into the IRIS Pipeline**



**\*\*Student Name:\*\*** Nitin Chauhan  

**\*\*Roll Number:\*\*** \`22f2001251\`  

**\*\*Email:\*\*** \`22f2001251\@ds.study.iitm.ac.in\`  

**\*\*Course:\*\*** Machine Learning Operations (MLOps) — IIT Madras BS Degree  

**\*\*Assignment:\*\*** Week 4 — Integrating CI into the IRIS Pipeline  

**\*\*Repository:\*\*** \`https\://github.com/IITM-22f2001251/22f2001251_MLOPS_WEEKLY_ASSIGNMENT\`  

**\*\*Target Duration:\*\*** 3 to 5 minutes  

**\*\*Target Screencast File Name:\*\*** \`22f2001251Assignment4SEPT2026_MLOps.mp4\`



\---



**## Rubric Breakdown Checklist (A through J)**



\- [x] **\*\*A. Explaining the Problem Statement\*\***

\- [x] **\*\*B. Explaining your approach to reach the objective\*\***

\- [x] **\*\*C. Explaining and demonstrating the configuration of cloud compute setup\*\***

\- [x] **\*\*D. Explaining Input files/data\*\***

\- [x] **\*\*E. Explaining and demonstrating sequence of actions performed\*\***

\- [x] **\*\*F. Exhaustive explanation of scripts/code and its objective\*\***

\- [x] **\*\*G. Errors encountered in the process and how they were overcome\*\***

\- [x] **\*\*H. Working demonstration of your pipeline in GCP / GitHub Actions Environment\*\***

\- [x] **\*\*I. Explaining output files/data\*\***

\- [x] **\*\*J. Learnings from this Assignment\*\***



\---



**## Detailed Word-by-Word Script with Visual Cues**



**### [0:00 - 0:30] A. Explaining the Problem Statement**

\* **\*\*🖥️ Screen Action:\*\*** Display the GitHub repository homepage and README.md header showing student details: Nitin Chauhan (\`22f2001251\`).

\* **\*\*🎙️ Spoken Dialogue:\*\***

\> "Hello everyone, my name is Nitin Chauhan, Roll Number 22f2001251, enrolled in the IIT Madras BS Degree in Data Science and Applications. This is my video screencast for the Week 4 MLOps graded assignment: Integrating Continuous Integration into the IRIS Pipeline.  

\>  

\> In Weeks 1 through 3, we built our cloud pipeline on Vertex AI, tracked data and models using Data Version Control (DVC) backed by Google Cloud Storage, and integrated Feast for feature serving. However, every time code is pushed, there was no automated mechanism verifying whether data invariants hold or if model accuracy degraded. Continuous Integration solves this by automatically pulling versioned artifacts via DVC, executing validation and evaluation tests, and publishing diagnostic reports directly to pull requests before merging."



\---



**### [0:30 - 0:55] B. Explaining Your Approach to Reach the Objective**

\* **\*\*🖥️ Screen Action:\*\*** Display the architecture flowchart in \`README.md\` or the terminal.

\* **\*\*🎙️ Spoken Dialogue:\*\***

\> "My approach establishes an end-to-end quality gate architecture using GitHub Actions, DVC, Pytest, and Continuous Machine Learning (CML):  

\> 1. **\*\*Automated Triggers:\*\*** CI triggers on every \`push\` and \`pull_request\` across all branches.  

\> 2. **\*\*DVC Artifact Pull:\*\*** The runner authenticates and executes \`dvc pull\` to fetch versioned data (\`data/iris.csv\`) and model binaries (\`models/model.joblib\`) from our GCS remote.  

\> 3. **\*\*Pytest Quality Gates:\*\*** Runs two specialized test suites comprising 17 automated unit tests for data invariants and model quality.  

\> 4. **\*\*CML Feedback Loop:\*\*** Evaluates predictions, creates a publication-grade markdown report, and posts it as an automated comment on the Pull Request.  

\> 5. **\*\*Quality-Gated Merge:\*\*** Code is only merged into \`main\` after all quality gates pass."



\---



**### [0:55 - 1:20] C. Configuration of Cloud Compute Setup**

\* **\*\*🖥️ Screen Action:\*\*** Show Google Cloud Console / Vertex AI Workbench instance details and GitHub Actions workflow environment.

\* **\*\*🎙️ Spoken Dialogue:\*\***

\> "Our cloud infrastructure and CI environment are configured as follows:  

\> - **\*\*Compute Environment:\*\*** Google Cloud Vertex AI user-managed Workbench instance \`instance-20261011-192557\` in zone \`us-central1-a\` (Project \`88792490605\` / \`project-97a8c7d5-b469-40bc-80c\`).  

\> - **\*\*Cloud Storage:\*\*** Bucket \`gs\://mlops-assignment-iitm\` hosting our DVC remote store at \`week_2/dvc_store\`.  

\> - **\*\*CI Runner:\*\*** GitHub Actions \`ubuntu-latest\` running Python 3.11 with \`pytest\`, \`dvc\`, \`dvc-gs\`, and \`setup-cml\@v2\`.  

\> - **\*\*Permissions:\*\*** Granted \`pull-requests: write\`, \`contents: write\`, and \`issues: write\` for automated CML reporting."



\---



**### [1:20 - 1:45] D. Explaining Input Files & Data**

\* **\*\*🖥️ Screen Action:\*\*** Show \`data/iris.csv.dvc\` and \`models/model.joblib.dvc\` in the editor or terminal.

\* **\*\*🎙️ Spoken Dialogue:\*\***

\> "The input artifacts are version-controlled using DVC pointer files:  

\> - **\*\*Dataset (\`data/iris.csv\`):\*\*** 150 biological observations with 4 numerical features—sepal length, sepal width, petal length, and petal width—and the target \`species\` (Setosa, Versicolor, Virginica). It is tracked by \`data/iris.csv.dvc\` with MD5 hash \`843050135e5a83df3b24e72160180706\`.  

\> - **\*\*Model Binary (\`models/model.joblib\`):\*\*** Serialized Decision Tree classifier tracked by \`models/model.joblib.dvc\` with MD5 hash \`01b7a2ebc28e50874649bc9d92f0001d\`.  

\>  

\> Only the lightweight pointer files are checked into Git, while the actual artifacts reside in GCS and are materialized during CI via \`dvc pull\`."



\---



**### [1:45 - 2:20] E. Sequence of Actions Performed**

\* **\*\*🖥️ Screen Action:\*\*** Show git log or branch structure (\`git log --oneline -n 6\`).

\* **\*\*🎙️ Spoken Dialogue:\*\***

\> "The exact sequence of actions performed was:  

\> 1. Created \`tests/test_data_validation.py\` containing 8 data invariant tests.  

\> 2. Created \`tests/test_model_evaluation.py\` containing 9 model quality gate tests with a 90% threshold.  

\> 3. Configured \`.github/workflows/ci.yml\` defining the complete GitHub Actions pipeline with DVC pull, Pytest, and CML reporting.  

\> 4. Enabled unrestricted workflow triggers for every push and pull request across all branches.  

\> 5. Created \`generate_cml_report.py\` to calculate accuracy, precision, recall, F1, and the confusion matrix.  

\> 6. Opened Pull Request #3 from \`week_4\` to \`main\`, verified the automated CI run and CML comment, and completed the merge."



\---



**### [2:20 - 2:50] F. Exhaustive Explanation of Scripts & Code**

\* **\*\*🖥️ Screen Action:\*\*** Open \`tests/test_data_validation.py\`, \`tests/test_model_evaluation.py\`, and \`.github/workflows/ci.yml\`.

\* **\*\*🎙️ Spoken Dialogue:\*\***

\> "Let's review the core scripts:  

\> - **\*\*\`tests/test_data_validation.py\`:\*\*** \`TestIrisDataSchemaAndIntegrity\` checks file existence, mandatory columns, 100% zero null values, continuous float datatypes, positive measurements (>0.0), botanical range intervals, and valid class taxonomies.  

\> - **\*\*\`tests/test_model_evaluation.py\`:\*\*** \`TestIrisModelQualityGates\` verifies model deserialization, batch inference alignment, and enforces that Accuracy, Precision, Recall, and F1-Score all exceed the 90% operational benchmark. It also includes \`test_regression_guard_catches_degraded_model\` to verify that a defective dummy classifier triggers an explicit assertion failure.  

\> - **\*\*\`generate_cml_report.py\`:\*\*** Generates \`cml_report.md\` formatted with GitHub Flavored Markdown for PR comments."



\---



**### [2:50 - 3:20] G. Errors Encountered in the Process & How They Were Overcome**

\* **\*\*🖥️ Screen Action:\*\*** Show terminal or workflow file highlighting error handling steps.

\* **\*\*🎙️ Spoken Dialogue:\*\***

\> "During implementation, we addressed two practical engineering hurdles:  

\> 1. **\*\*DVC Remote Access in CI Runners:\*\*** In headless CI environments without interactive GCP credentials, \`dvc pull\` can fail. We resolved this by configuring both service account key authentication and an intelligent fallback via \`sync_cache.py\`, guaranteeing that DVC artifacts are reliably materialized on every run.  

\> 2. **\*\*CSV Header Encoding Variations:\*\*** Byte Order Marks (BOM) in CSV files can corrupt column naming. In \`tests/conftest.py\`, we implemented sanitization stripping \`\\\ufeff\` characters to ensure robust column matching across platforms."



\---



**### [3:20 - 4:15] H. Working Demonstration of Pipeline (CORE DEMO)**

\* **\*\*🖥️ Screen Action:\*\***&#x20;

  1. Switch to GitHub Actions tab showing completed run #41343506818 for PR #3.

  2. Click into the run and expand the steps: "Pull Versioned Data and Model Artifacts", "Execute Pytest Validation", "Generate Evaluation Metrics", and "Post CML Report".

  3. Switch to Pull Request #3 conversation showing the CML comment and Merged status.

\* **\*\*🎙️ Spoken Dialogue:\*\***

\> "Now let's demonstrate the live pipeline on GitHub Actions:  

\>  

\> Here in the Actions tab, you can see Workflow Run #41343506818 triggered automatically by Pull Request #3 from \`week_4\` to \`main\`.  

\>  

\> Inspecting the step logs:  

\> - **\*\*Pull Versioned Data & Model Artifacts:\*\*** DVC pulls \`data/iris.csv\` and \`models/model.joblib\`. Both files are verified non-empty.  

\> - **\*\*Execute Pytest Suite:\*\*** All 17 unit tests run in 0.4 seconds—8 data validation tests and 9 model quality gate tests—all passing with green status!  

\> - **\*\*Generate Evaluation Metrics & CML Report:\*\*** \`generate_cml_report.py\` generates the markdown summary.  

\> - **\*\*Post CML Report:\*\*** CML publishes the diagnostic report directly to the PR.  

\>  

\> Now switching to Pull Request #3: Here is the automated comment posted by \`github-actions[bot]\`. It displays our Quality Gate Performance Matrix with **\*\*97.33% Accuracy\*\***, **\*\*0.9738 Precision\*\***, **\*\*0.9733 Recall\*\***, and **\*\*0.9733 F1\*\***, along with the per-class breakdown and confusion matrix.  

\>  

\> With all quality gates satisfied, Pull Request #3 was successfully merged into \`main\`!"



\---



**### [4:15 - 4:40] I. Explaining Output Files & Data**

\* **\*\*🖥️ Screen Action:\*\*** Show \`cml_report.md\` in repository and the merged commit on \`main\`.

\* **\*\*🎙️ Spoken Dialogue:\*\***

\> "The key outputs produced by this pipeline include:  

\> 1. **\*\*\`cml_report.md\`:\*\*** The persistent markdown diagnostic record containing our metric thresholds and confusion matrix.  

\> 2. **\*\*PR #3 Discussion Comment:\*\*** A permanent audit record in the GitHub Pull Request conversation.  

\> 3. **\*\*Interactive Notebook:\*\*** \`22f2001251Assignment4SEPT2026_MLOps.ipynb\` providing a reproducible walkthrough of the entire pipeline."



\---



**### [4:40 - 5:00] J. Learnings from this Assignment**

\* **\*\*🖥️ Screen Action:\*\*** Return to GitHub repository main page.

\* **\*\*🎙️ Spoken Dialogue:\*\***

\> "In summary, the key takeaways from Week 4 are:  

\> 1. How Continuous Integration serves as the automated quality safeguard for machine learning pipelines.  

\> 2. Integrating DVC into GitHub Actions ensures tests always run on exact, versioned artifacts.  

\> 3. CML brings transparent, verifiable evaluation reports directly into developer code reviews.  

\>  

\> Thank you!"



\---



**## Submission Summary Checklist**

\- **\*\*Student ID:\*\*** \`22f2001251\`

\- **\*\*File Name:\*\*** \`22f2001251Assignment4SEPT2026_MLOps.mp4\`

\- **\*\*Branch:\*\*** \`week_4\` (merged into \`main\` via PR #3)

\- **\*\*Collaborator:\*\*** \`IITMBSMLOps\` (\`da5014_1\@study.iitm.ac.in\`)
