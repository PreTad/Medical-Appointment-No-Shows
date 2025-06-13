# Medical-Appointment-No-Shows
""

## Data Cleaning and Preparation

The initial steps involved checking for missing values and duplicated rows in the dataset.

*   **Missing Values and Duplicates:** The dataset was checked for missing values and duplicates. No duplicate rows were found. A small number of missing values were present in several columns (`Age`, `Neighbourhood`, `Scholarship`, `Hipertension`, `Diabetes`, `Alcoholism`, `Handcap`, `SMS_received`, `No-show`).
*   **Handling Negative Age Values:** Rows with negative age values were identified and removed as they represent inconsistent data.
*   **Converting Date Columns and Calculating Waiting Time:** The 'ScheduledDay' and 'AppointmentDay' columns, initially strings, were converted to datetime objects to allow for temporal calculations. A new feature, 'Waiting Time', was created by calculating the difference in days between the 'AppointmentDay' and 'ScheduledDay'.
*   **Removing Inconsistent Appointments:** Rows where the 'AppointmentDay' was chronologically before the 'ScheduledDay' were identified and removed as they represent illogical data entries.
""
