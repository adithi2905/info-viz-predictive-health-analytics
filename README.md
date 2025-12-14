---

# **A Machine Learning–Driven Visualization of U.S. Life Expectancy: Chronic Disease Burden, Behavioral Choices, Environment, and Population by State**

Built interactive, state-level visualizations of U.S. life expectancy and modeled the influence of chronic diseases, personal behaviors, environmental conditions, and population factors using machine learning.

Dashboard Links
Past and Current trends: https://app.powerbi.com/view?r=eyJrIjoiYmNjM2M3MDctYjhjMy00YzdhLTljZmEtNjlkMDBmMmFjMmYzIiwidCI6IjExMTNiZTM0LWFlZDEtNGQwMC1hYjRiLWNkZDAyNTEwYmU5MSIsImMiOjN9
Predicted Future Trends: https://app.powerbi.com/view?r=eyJrIjoiNDQyMzFkMWEtOTcxYi00NmQwLThlNTYtNTkxOTUyMDVlZDUwIiwidCI6IjExMTNiZTM0LWFlZDEtNGQwMC1hYjRiLWNkZDAyNTEwYmU5MSIsImMiOjN9

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
Source: Air Quality Index by State (1980–2022) – https://www.kaggle.com/datasets/adampq/air-quality-index-by-state-1980-2022

<img width="156" height="134" alt="image" src="https://github.com/user-attachments/assets/64e69556-2be0-41b3-a1d6-f776d0a690eb" />

---

### **Health_care_access.csv**
Healthcare Access and Quality Index: https://www.kaggle.com/datasets/valchovalev/healthcareaccessandqualityindex

<img width="151" height="113" alt="image" src="https://github.com/user-attachments/assets/d04b47e3-7e66-4a34-b943-0fbe271928ae" />

These datasets were sourced from Kaggle and combined with the client-provided datasets after removing columns that were not relevant to the project.

---

## Data Integration

The final dataset combines patient profiles, medical history, and healthcare events with environmental and healthcare access data to create a more comprehensive view of health outcomes.

While the client-provided datasets focus on patients’ personal choices, medical history, and healthcare events, these factors alone do not fully explain disease prevalence or life expectancy. Broader contextual factors - such as environmental pollution, population characteristics, and access to healthcare - also play a significant role in influencing health outcomes. To capture this broader context, we integrated two Kaggle datasets at the state and year level, retaining only relevant fields and discarding unnecessary attributes. The resulting dataset is enriched with both individual-level and contextual information and is structured as shown below.

<img width="182" height="131" alt="image" src="https://github.com/user-attachments/assets/76102e90-3a74-4982-90d7-ad6e659f204b" />

---

## Life Expectancy and Longevity Estimation Strategy

The goal of this analysis is to understand life expectancy and survival patterns associated with chronic conditions across various U.S. states, and to leverage historical and current trends to forecast future patterns using machine learning models.

Since life expectancy information was implicit in the client-provided data, we derived longevity patterns using available timestamps. Specifically, we extracted the year from the event_date column in the health_events dataset and the year from the diagnosis_date column in the medical history dataset.

For simplification, and due to the absence of explicit event–diagnosis linkage, longevity was computed as the absolute difference between the event year and the diagnosis year, regardless of whether the healthcare event occurred before or after the diagnosis. The cases with outcome fatal or recovered were considered for this analysis and the ongoing cases were deliberately ignored as the status of the condition remains unclear. While this assumption may not fully reflect real-world clinical timelines—and patients may be associated with multiple chronic conditions that correspond to different healthcare events—it was necessary given the structure of the mocked-up data.

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

## Prediction Models and Forecasting Approach

To extend descriptive longevity analysis into forward-looking insights, machine learning–based predictive models were incorporated. A CatBoost forecasting model was used to predict short- and medium-term disease prevalence trends across states. This model was selected for its ability to handle heterogeneous feature types, capture non-linear relationships, and perform robustly on structured health and environmental data. Historical prevalence, temporal features, environmental indicators (such as AQI), healthcare access metrics, and demographic attributes were used as inputs to generate one-year and five-year prevalence forecasts.

In addition to prevalence forecasting, a Random Survival Forest (RSF) model was employed to estimate patient survival patterns and risk over time. RSF is well-suited for censored survival data and enables modeling of complex interactions between clinical, demographic, and environmental variables without strong parametric assumptions. The model was trained using derived longevity measures, disease severity, health conditions, and contextual factors to estimate survival probabilities and risk stratification across different time horizons.

Together, these models complement the dashboard’s descriptive visualizations by providing predictive insights into future disease burden and survival outcomes. While the predictions are based on historical trends and modeled assumptions, they offer valuable early signals for public health planning, resource allocation, and comparative risk assessment across states. Continuous retraining and incorporation of updated data are expected to further improve model accuracy in future iterations.

---

## Conclusion

This project brings together individual-level health records and broader state-level context to create a richer, more interpretable view of life expectancy patterns across the U.S. By integrating patient profiles, medical history, and healthcare events with environmental (AQI) and healthcare access indicators, the dashboard enables state-by-state comparison of how chronic disease burden, behavioral choices, and external conditions relate to longevity outcomes. Because the client-provided data is mocked and does not explicitly link events to specific conditions, we made transparent simplifying assumptions to derive consistent longevity measures and support meaningful visual exploration.

Beyond descriptive insights, the forecasting components extend the dashboard into a forward-looking tool. CatBoost-based prevalence forecasting provides short- and medium-term signals on potential future disease burden, while the Random Survival Forest model offers a way to estimate survival risk patterns using the derived longevity proxy and contextual features. Together, these outputs support comparative analysis and early planning—while also highlighting opportunities for future improvement, such as incorporating per-capita normalization, stronger event–condition linkage, and validation with real clinical timelines.


