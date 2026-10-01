# Integrating-Machine-Learning-To-Conveyancing
# Project Overview
This is a Python machine learning model created to classify the responses made to a conveyancing enquiry form. Through the usage of both "valid" and "invalid" answers to train the CatBoost decision tree model on, the algorithm can recognize the answer patterns to questions to see if the section was answered correctly or not. After that, the user can manually choose an answer pattern on the user interface and have it evaluate to see if this section of the enquiry form has valid answers, answers that require a follow-up check with the client, or invalid answers.

# User Interface
<img width="732" height="552" alt="Screenshot 2026-07-13 122648" src="https://github.com/user-attachments/assets/48547bcb-c194-4539-a8a2-3be7e3285075" />

# Work Process
The first thing to note is that this project used the TA6 Law Society Property Information Form (6th edition) (2025) as a reference the dataset: <img width="942" height="1455" alt="EDITABLE TA6 Section 2_page-0001" src="https://github.com/user-attachments/assets/e3da635a-b894-4b45-962e-79c1ed5f7ad5" />

This example image is just one page of the enquiry form, showcasing one section of it. Much of the work within this project is about translating this form into a format that can be read by Python algorithm in order to create a classification response system that can determine how well an enquiry section was answered.

## Generating Dataset
Each questions of the form act as a column for the dataset, and any possible answers a question can have is a potential value for the column. For example, 2.1a could either have "Seller", "Shared", "Neighbor", "Not known", or just no answer at all as a potential value. This had to be "translated" into Microsoft Excel as a dataset for the model to use. This is shown as such:
<img width="1740" height="655" alt="Screenshot 2026-10-01 144430" src="https://github.com/user-attachments/assets/10d7f54b-7266-4e84-8d6a-8c85532f1aac" />


Notice how each questions (and its part) of the section is translated into a column within the dataset. Each columns has an Excel formula that randomly picks between possible answer values based on the question it's referencing. That's why you see random but distinct outputs within each of the columns. Along with the question columns, each sections also has an output column at the end to put in the whichever classification results best fit the answer patterns along the row. This type of generation is done by a custom Python algorithm that is shown within the next chapter of this repository. 
## Modeling
### Generating Test Outputs
In order to generate the test values to compare the training values to for the model, a Python rule-based system was created for this purpose. The output column would be given a classification value of "Valid," "Follow-up Check," or "Invalid" based on how the answer patterns were answered. The coding is shown as such:
<img width="1872" height="660" alt="Screenshot 2026-06-29 091853" src="https://github.com/user-attachments/assets/1e99a174-a417-401d-a776-c04d3a71531e" />

### Training & Testing
Since the dataset is comprised entirely of categorical features, the model that was chosen for the task of classifying answer patterns was a CatBoost decision tree model. Due to the length of the enquiry form, only five (sub)sections were chosen for this model for convenience sake and to see how the model fares against different kinds of sections.

