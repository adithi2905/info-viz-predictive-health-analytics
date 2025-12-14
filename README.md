---

# **A Machine Learning–Driven Visualization of U.S. Life Expectancy: Chronic Disease Burden, Behavioral Choices, Environment, and Population by State**

Built interactive, state-level visualizations of U.S. life expectancy and modeled the influence of chronic diseases, personal behaviors, environmental conditions, and population factors using machine learning.

---

## Client-Provided Datasets

### **ENGR-E 483_583_Patients_Data.xlsx**

This dataset contains patient profiles with unique records for each patient.

<img width="332" height="299" alt="Patients" src="https://github.com/user-attachments/assets/e9c68033-7909-4de9-b73f-4f965277da2e" />

---

### **ENGR-E 483_583_Medical_History_final.xlsx**

This dataset contains diagnosis records associated with patients and captures their medical history.

<img width="395" height="157" alt="medical_records" src="https://github.com/user-attachments/assets/420902e8-ea15-45ea-9f36-dd719f718ae7" />

---

### **ENGR-E 483_583_Health_Events_cleaned.xlsx**

This dataset includes health events such as hospitalizations and other medical visits associated with patients.

If a patient is diagnosed with a disease, it is assumed that the reason for the health event could be related to the health condition they are suffering from. While this may not be a fully valid real-world assumption, it was made to simplify the analysis, as the data is mocked-up.

If there are no records in the medical history file, we assume that the patient is not suffering from a chronic health condition. In such cases, the healthcare visit is assumed to be due to an acute condition or an accident.

<img width="349" height="194" alt="health_events" src="https://github.com/user-attachments/assets/5a27f6fc-f119-494f-a8fe-26dfd1ecd1eb" />

---

## Kaggle Datasets

### **AQI By State 1980–2022.csv**

<img width="156" height="134" alt="image" src="https://github.com/user-attachments/assets/64e69556-2be0-41b3-a1d6-f776d0a690eb" />

---

### **Health_care_access.csv**

<img width="151" height="113" alt="image" src="https://github.com/user-attachments/assets/d04b47e3-7e66-4a34-b943-0fbe271928ae" />

These datasets were sourced from Kaggle and combined with the client-provided datasets after removing columns that were not relevant to the project.

---

## Data Integration

The final dataset combines patient profiles, medical history, and health events with environmental and healthcare access data to make the dataset richer.

The client-provided datasets focus on patients’ choices, medical history, and healthcare events. However, these are not the only factors that determine disease prevalence and life expectancy. Environmental factors such as pollution, population characteristics, and healthcare access also contribute to life expectancy and the likelihood of chronic diseases.

<img width="182" height="131" alt="image" src="https://github.com/user-attachments/assets/76102e90-3a74-4982-90d7-ad6e659f204b" />

---

## Life Expectancy and Longevity Estimation Strategy

The goal of this analysis is to understand life expectancy and survival patterns associated with chronic conditions across various U.S. states, and to leverage historical and current trends to forecast future patterns using machine learning models.

Since life expectancy information was implicit in the client-provided data, we derived longevity patterns using available timestamps. Specifically, we extracted the year from the event_date column in the health_events dataset and the year from the diagnosis_date column in the medical history dataset.

For simplification, and due to the absence of explicit event–diagnosis linkage, longevity was computed as the absolute difference between the event year and the diagnosis year, regardless of whether the healthcare event occurred before or after the diagnosis. While this assumption may not fully reflect real-world clinical timelines—and patients may be associated with multiple chronic conditions that correspond to different healthcare events—it was necessary given the structure of the mocked-up data.

Because the health events dataset does not explicitly associate individual events with specific chronic conditions, this assumption was adopted to enable consistent estimation of longevity patterns and downstream analysis.

---

## Dashboard Design and Key Visualizations

The dashboard was designed to show the three factors that influence life expectancy. One of the key aspects focuses on the personal choices of individuals, such as smoking, drinking, and opioid addiction, analyzed among people with a sedentary lifestyle as well as those who are physically active.

We also visualized opioid addiction among people living alone. These insights can be filtered across various states and viewed over a range of years using a year slider or slicer.

We further explored how air quality varies with changes in population across states. In future iterations, we plan to replace total population with per-capita measures to provide a more normalized and meaningful comparison.

To analyze health outcomes in more detail, we examined the relationship between longevity and the number of chronic disease cases using a combination of line charts and bar graphs across various states. This helped identify trends and variations in longevity patterns associated with different chronic conditions.

Additionally, we analyzed how disease severity influences outcomes, providing insight into how more severe conditions correlate with changes in longevity.

Finally, we computed the overall average longevity and used a performance indicator to visualize how longevity is distributed across different states, enabling comparative analysis at the state level.

---
