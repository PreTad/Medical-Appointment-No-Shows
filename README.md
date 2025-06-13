# Medical-Appointment-No-Shows

## Dataset

The dataset used in this project is the 'Medical Appointment No Shows' dataset, obtained from Kaggle. It contains information about medical appointments in Brazil and includes details such as patient characteristics, appointment details, and whether the patient showed up for the appointment.

## Data Cleaning and Preparation

The initial steps involved checking for missing values and duplicated rows in the dataset.

*   **Missing Values and Duplicates:** The dataset was checked for missing values and duplicates. No duplicate rows were found. A small number of missing values were present in several columns (`Age`, `Neighbourhood`, `Scholarship`, `Hipertension`, `Diabetes`, `Alcoholism`, `Handcap`, `SMS_received`, `No-show`).
*   **Handling Negative Age Values:** Rows with negative age values were identified and removed as they represent inconsistent data.
*   **Converting Date Columns and Calculating Waiting Time:** The 'ScheduledDay' and 'AppointmentDay' columns, initially strings, were converted to datetime objects to allow for temporal calculations. A new feature, 'Waiting Time', was created by calculating the difference in days between the 'AppointmentDay' and 'ScheduledDay'.
*   **Removing Inconsistent Appointments:** Rows where the 'AppointmentDay' was chronologically before the 'ScheduledDay' were identified and removed as they represent illogical data entries.
## Exploratory Data Analysis (EDA)

Exploratory Data Analysis was conducted to understand the dataset's characteristics and identify potential relationships with the 'No-show' variable.

*   **Feature Distributions:** Histograms of numerical features revealed that 'Age' is right-skewed, indicating a larger number of younger patients. Other numerical features like 'Scholarship', 'Hipertension', 'Diabetes', 'Alcoholism', and 'SMS_received' are binary (0 or 1) and their distributions show the counts of each category. 'PatientId' and 'AppointmentID' are identifiers and not used for analysis.
*   **No-show by Gender:** A countplot showed the distribution of 'No-show' across genders. While more females had appointments overall, the proportion of no-shows appeared similar between genders. However, the total number of female patients is significantly higher, which biases the raw counts.
*   **No-show by Neighbourhood:** The relationship between 'No-show' and the top 10 most frequent 'Neighbourhoods' was visualized. Some neighbourhoods showed higher counts of both attended and missed appointments, highlighting the varying volume of appointments in different areas. No specific neighbourhood stood out as having a disproportionately high no-show rate compared to others in the top 10.
*   **No-show by Waiting Time:** A boxplot illustrating the relationship between 'Waiting Time' (the number of days between scheduling and appointment) and 'No-show' indicated that patients with longer waiting times were generally more likely to miss their appointments. The boxplot also showed a significant number of outliers with very long waiting times.
## Modeling

To predict the 'No-show' outcome, several machine learning models were employed:

*   **Gradient Boosting:** A powerful ensemble method that builds trees sequentially, with each new tree correcting errors of the previous ones.
*   **Logistic Regression:** A linear model used for binary classification, which estimates the probability of the target variable.
*   **Neural Network:** A simple sequential neural network with dense layers and a sigmoid activation function for binary output.

During the analysis, it was observed that the target variable, 'No-show', was imbalanced, with a significantly higher number of patients who showed up compared to those who did not. To address this class imbalance and prevent the models from being biased towards the majority class, **Random Over-Sampling** was applied to the training dataset using the `RandomOverSampler` from the `imblearn` library. This technique duplicates random instances of the minority class to balance the class distribution in the training data.
## Results and Evaluation

After training the models, their performance was evaluated using accuracy, precision, recall, and F1-score.

*   **Accuracy:** Represents the overall correctness of the model.
*   **Precision:** The ability of the model to return only relevant instances (out of all predicted positive cases, how many were actually positive). In this context, it's the proportion of predicted no-shows that were actual no-shows.
*   **Recall:** The ability of the model to find all relevant instances (out of all actual positive cases, how many were predicted correctly). In this context, it's the proportion of actual no-shows that the model correctly identified.
*   **F1-score:** The harmonic mean of precision and recall, providing a balanced measure of the model's performance.

Due to the imbalanced nature of the target variable ('No-show'), focusing solely on accuracy can be misleading. A high accuracy might simply indicate that the model is good at predicting the majority class (patients who show up). Therefore, it is crucial to examine the precision, recall, and F1-score for the minority class ('No-show') to understand how well the model identifies patients who will miss their appointments.

Here's a summary of the model performances:

*   **Gradient Boosting:**
    *   Accuracy: Approximately 61.1%
    *   Classification Report (Minority Class '1' - No-show): Precision: 0.27, Recall: 0.52, F1-score: 0.35
*   **Logistic Regression:**
    *   Accuracy: Approximately 59.1%
    *   Classification Report (Minority Class '1' - No-show): Precision: 0.25, Recall: 0.50, F1-score: 0.33
*   **Neural Network:**
    *   Accuracy: Approximately 76.5%
    *   Classification Report (Minority Class '1' - No-show): Precision: 0.32, Recall: 0.13, F1-score: 0.18

While the Neural Network achieved the highest overall accuracy, its recall and F1-score for the 'No-show' class are significantly lower compared to Gradient Boosting and Logistic Regression. This suggests that although the Neural Network is better at correctly predicting patients who show up, it struggles to identify actual no-shows. Gradient Boosting and Logistic Regression, despite lower overall accuracy, have better recall for the minority class, meaning they are more effective at capturing a larger portion of the actual no-shows.

The key takeaway is that for this problem, maximizing the correct identification of no-shows (high recall for the minority class) is often more valuable than overall accuracy. The models, particularly the Gradient Boosting and Logistic Regression models after oversampling, show some ability to predict no-shows, but there is room for improvement in their precision and F1-score for the minority class.
## Conclusion

This project analyzed the Medical Appointment No-Shows dataset to predict patient attendance. Key insights were gained regarding the distribution of features, the relationship between 'No-show' and factors like 'Waiting Time', and the performance of different classification models.

The data cleaning process addressed issues like negative age values and inconsistent appointment dates, and a 'Waiting Time' feature was engineered, which was found to be a significant factor in no-shows.

Exploratory data analysis revealed that longer waiting times are associated with a higher likelihood of no-shows. The dataset's class imbalance was identified as a challenge for modeling.

Several models were trained, and Random Over-Sampling was used to handle the class imbalance. While the Neural Network achieved the highest overall accuracy, Gradient Boosting and Logistic Regression demonstrated better recall for the minority class ('No-show'), indicating a better ability to identify patients who would miss appointments. The choice of the best model depends on whether the priority is overall accuracy or minimizing missed no-shows.

Potential next steps to improve the prediction of no-shows include:

*   Exploring other features or creating more complex engineered features.
*   Trying different oversampling or undersampling techniques, or using techniques like SMOTE.
*   Tuning the hyperparameters of the models for better performance.
*   Investigating other classification algorithms suitable for imbalanced datasets.
*   Analyzing the impact of 'Neighbourhood' in more detail, potentially grouping less frequent neighbourhoods or using encoding techniques that capture spatial relationships.
