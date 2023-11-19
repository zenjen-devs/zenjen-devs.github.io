[Back](https://zenjen-devs.github.io)

# Predicting Failures in High-Risk Production: Aircraft Engines

![image](https://github.com/zenjen-devs/zenjen-devs.github.io/assets/84609216/c4bb9213-a0f0-495a-bade-8b65391429ca)

[View Repository](https://github.com/zenjen-dev/deep-learning_predicting-failures/blob/main/DeepLearning_PredictiveMaintenance.ipynb) <br>

*Note: This portfolio section is currently in progress. Please see the project repository linked above for current work status.*

<h3> Project Summary </h3>

In the high-stakes world of defense aerospace manufacturing, ensuring the reliability and safety of hardware is paramount. This deep learning project employs Long Short-Term Memory (LSTM) networks (Tensorflow/Keras libraries for Python) to predict failures in a high-risk production environment where maintenance windows are dynamic, thus requiring robust modelling and hyper-parameter tuning. The aim is to proactively identify potential issues, reduce downtime costs, and increase servicability of assets.

**Results**: The model performance metrics indicate that the LSTM algorithm correctly identifies failures in dynamic operational windows 97.6% of the time. Considering that our specific goal is high precision in predicting failures, false negatives are more costly than false positives. 
To ensure the model is robust to real-world scenarios, in the next steps we'll need to evaluate model performance with a larger training data set or through upsampling.

<h3> Project Details: Exploratory Data Analysis </h3>

**Data Collection and Preprocessing:**
For this project, the data source is imported NASA sensor readings from mission-critical asset production. The sensor data was cleaned, normalized, and preprocessed to ensure data integrity. A sample of the visualized sensor data is shown below:
<br>

![Sensors_EDA](https://github.com/zenjen-devs/zenjen-devs.github.io/assets/84609216/d4d91dc9-d2bf-4426-ad6f-99ec2ab864c7)
  
Data Source: [NASA](https://data.nasa.gov)


### Insights from EDA

**Variability Across Engines:** There is variability in sensor readings across different engines, even for the same sensor. This could be due to different operating conditions, usage patterns, or inherent differences between engines.

**Sensor Behavior:** The behavior of each sensor can be quite different. Some sensors may show a lot of noise (frequent up and down fluctuations), while others may have a smoother trend.

**Early Warning Signs:** Some sensors may provide signs of a potential failure, evident in changes in their readings that precede a failure. This would be valuable for predictive maintenance.

**Operational Baselines:** It's possible to identify a baseline of normal operation for each sensor, against which deviations can be compared to detect anomalies. This is valuable to adjust maintenance tailored for each operators needs, and sustainment efforts to maintain servicability of hardware.
<br>

![PredictiveMaint_CorrMatrix](https://github.com/zenjen-devs/zenjen-devs.github.io/assets/84609216/54d47003-d9e1-4071-b0c6-607009987a42)

**Correlation Matrix of Sensor Readings and Settings:** The heatmap indicates some sensors are highly correlated with each other, which could be due to underlying physical relationships or redundancies in what is being measured. Strongly correlated sensors may provide overlapping information and could be candidates for dimensionality reduction techniques.

### Predictive Modeling with LSTM Network

**A Novel Approach to Feature Engineering:**
The benefit of applying deep learning in the predictive maintenance domain is that these networks can automatically extract the most impactful features from the data, eliminating the need for manual feature engineering. The idea of using LSTMs is to let the model extract abstract features out of the sequence of sensor values in the window, rather than engineering those manually. The expectation is that if there is a pattern in these sensor values within the window prior to failure, the pattern should be encoded by the LSTM.

![LSTM_SensorReadings](https://github.com/zenjen-devs/zenjen-devs.github.io/assets/84609216/f550ed65-f9fc-4827-89b3-c1df4b83f4d8)


**LSTM Model Architecture & Model Training/Validation:** In this phase, we performed the following:
   - Designed LSTM-based neural networks to capture temporal dependencies and patterns in the sensor data.
   - Explored various LSTM architectures and hyperparameters to optimize model performance.
   - Split the dataset into training, validation, and test sets to evaluate model generalization.
   - Employed techniques such as early stopping and dropout to mitigate overfitting.

**Performance Evaluation:**
Model performance was assessed using precision, recall, and F1-score to scrutinize prediction reliability. <br>

   ![image](https://github.com/zenjen-devs/zenjen-devs.github.io/assets/84609216/d776bfe9-22d8-49f1-b4b7-5c14802e0a27)
   <br>


   ![image](https://github.com/zenjen-devs/zenjen-devs.github.io/assets/84609216/ae2445e8-c165-4166-8039-ece055c91823)
     <br>
     
<br>

*Precision = 0.97*
<br>
When the LSTM model predicted an engine failure, it was correct 97% of the time.
<br>
<br>
*Recall = 0.91*
<br>
The LSTM model correctly identified 91% of all engine failures.
<br>
<br>
*F1-Score = 0.94*
<br> 
Considering that our specific goal is high precision in predicting failures, false negatives are more costly than false positives.
<br>
<br>

**Real-time Monitoring System:**
To integrate the model into the production process, we will implement a real-time monitoring system that provisions immediate alerts when potential engine failures are predicted.

**Integration with Maintenance Protocols:**
Upon completion of model validation and system implementation, we collaborated with service engineering teams to integrate predictive results into maintenance schedules, enabling proactive servicing and part replacement. <br>

By leveraging deep learning with LSTM networks, this project contributes to the enhanced safety and operational efficiency of high-risk aircraft engine production environments. Early detection of anomalies and potential failures minimizes downtime, reduces operational risks, and reinforces the commitment to safety and reliability in the aerospace industry.

**References:** [See Repository](https://github.com/zenjen-dev/deep-learning_predicting-failures/blob/main/DeepLearning_PredictiveMaintenance.ipynb) 
