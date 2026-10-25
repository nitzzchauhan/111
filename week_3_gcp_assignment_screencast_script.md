# Week 3 GCP Assignment — Screencast Script

**Graded Assignment 2 | September 2026**  
**Estimated duration:** 5–7 minutes

> Use this script while recording your 5–10 minute screencast. Demonstrate your actual GCP environment and replace any generic descriptions with your real resource names and results.

## 1. Introduction and Problem Statement

“Hello everyone. In this video, I will demonstrate my Graded Assignment 2 for Week 3, where I use Google Cloud Platform to identify the longest lines in a text file.

The objective is to create a Google Cloud Function that automatically triggers whenever a file is uploaded to a Google Cloud Storage bucket. The function downloads the file, identifies all lines having the maximum character length, prints the results in Cloud Logging, and saves the results back into the same bucket.”

## 2. Approach and Architecture

“My approach is event-driven and serverless. Instead of creating a virtual machine and running a script manually, I use Google Cloud Functions to process files automatically.

The workflow is:

1. Upload a text file to a Google Cloud Storage bucket.
2. The storage event triggers the Cloud Function.
3. The function downloads and reads the file.
4. Python identifies every line with the maximum character length.
5. The results are printed in Cloud Logging.
6. The results are saved to an output file in the same bucket.

The important point is that all processing takes place on GCP, and the function runs automatically in response to a storage event.”

## 3. Explain the Input File

**[Show `input.txt` in your project or GCS bucket.]**

“This is my input text file. It contains multiple lines of different character lengths. My objective is to identify the longest line or lines.

If multiple lines have the same maximum length, all of them must be reported. The comparison is based on character length, not the number of words.”

## 4. Demonstrate GCP Configuration

**[Open the Google Cloud Console and show the configured resources.]**

“First, I selected my GCP project and configured the required services. I created a Google Cloud Storage bucket to store the input and output files.

Next, I configured the Cloud Function with Python as the runtime and Cloud Storage as the event source. I selected the appropriate bucket and configured the function to trigger when a new object is created.

I also configured the necessary permissions so the function can read the input file, write the output file, and generate logs.

Since this is a serverless setup, I do not need to create a virtual machine or SSH into one. Google Cloud manages the compute infrastructure for me.”

## 5. Explain the Python Code

**[Open `main.py` and explain the main sections.]**

“The Python code contains the logic for processing the uploaded file.

First, the function receives the Cloud Storage event and extracts the bucket name and uploaded file name.

Second, it accesses the uploaded file using the Google Cloud Storage client library and downloads its content.

Third, it processes the text line by line and calculates the maximum character length. It then collects every line whose length matches that maximum. This ensures that ties are handled correctly.

Fourth, it prints the longest lines and their lengths so that the results can be inspected in Cloud Logging.

Finally, it creates an output file containing the results and uploads it to the same GCS bucket.

The `requirements.txt` file specifies the external Python dependencies required by the function.

The function is event-driven, so a new upload can initiate processing without manually running the Python script.”

## 6. Explain the Execution Sequence

**[Demonstrate the actual sequence in GCP.]**

“The sequence of actions performed was:

1. Create and configure the GCS bucket.
2. Upload the input text file.
3. Deploy the Cloud Function with the required Python code and dependencies.
4. Configure the Cloud Storage trigger.
5. Upload a new input file to trigger the function.
6. Open Cloud Logging to inspect the execution results.
7. Open the GCS bucket again and verify the generated output file.

I will now demonstrate this complete workflow in the live GCP environment.”

## 7. Errors Encountered and How They Were Handled

**[Mention only errors you actually encountered.]**

“During configuration and testing, I checked the function's deployment status, event trigger, permissions, and execution logs.

If an error occurs, Cloud Logging helps identify whether the issue is related to deployment, permissions, file access, or code execution. I would resolve the reported issue and upload a new input file to test the function again.

For this assignment, I will show any actual errors encountered and the corresponding fixes.”

## 8. Live Demonstration and Output Verification

**[Perform a fresh upload and show the resulting logs and file.]**

“Now I am uploading the input file to the configured GCS bucket.

This upload triggers the Cloud Function automatically. I will open Cloud Logging and show the printed results, including the longest line or lines and their character lengths.

Next, I will return to Cloud Storage and open the generated output file. The output contains all lines having the maximum character length.

This verifies that the function has processed the input, logged the results, and saved the output in the same bucket.”

## 9. Explain the Output Files

**[Show the input and generated output files in Cloud Storage.]**

“The input file contains the original text data. The output file contains the longest line or lines identified by the function.

I can compare the output with the input to verify that every line with the maximum character length has been included. Cloud Logging provides additional evidence that the function executed and printed the results.”

## 10. Learnings and Conclusion

“Through this assignment, I learned how to build an event-driven serverless application on Google Cloud Platform.

I understood how Cloud Storage events trigger Cloud Functions, how Python processes files stored in the cloud, how Cloud Logging helps monitor execution, and how processed results can be written back to Cloud Storage.

I also learned the importance of configuring permissions, validating outputs, and testing the complete pipeline in the cloud environment.

This concludes my demonstration of Graded Assignment 2 for Week 3. Thank you.”

---

## Recording Checklist

- [ ] Show the GCP project and Cloud Storage bucket.
- [ ] Show the input text file.
- [ ] Show the Cloud Function configuration, runtime, and trigger.
- [ ] Explain `main.py` and `requirements.txt`.
- [ ] Upload a fresh input file to trigger execution.
- [ ] Show the printed results in Logs Explorer.
- [ ] Show and open the generated output file in the same bucket.
- [ ] Explain any real errors and how they were resolved.
- [ ] Keep the screencast between 5 and 10 minutes and include clear audio.
- [ ] Ensure the demonstration visibly takes place in GCP; local execution alone is not sufficient.
