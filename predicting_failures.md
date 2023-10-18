[Back](https://zenjen-devs.github.io)

# Predicting Failures in High-Risk Production: Aircraft Engines

![image](https://github.com/zenjen-devs/zenjen-devs.github.io/assets/84609216/c4bb9213-a0f0-495a-bade-8b65391429ca)

[View Repository](https://github.com/zenjen-dev/deep-learning_predicting-failures/blob/main/DeepLearning_PredictiveMaintenance.ipynb) <br>

*Note: This portfolio section is currently in progress. Please see the project repository linked above for current work status.*

<h3> Project Summary </h3>

In the high-stakes world of defense aerospace manufacturing, ensuring the reliability and safety is paramount. This deep learning project employs Long Short-Term Memory (LSTM) networks (Tensorflow/Keras libraries for Python) to predict failures in a high-risk production environment where maintenance windows are dynamic, thus requiring robust modelling and hyper-parameter tuning. The aim is to proactively identify potential issues, reduce downtime costs, and increase servicability of assets.

**Results**: The model performance metrics indicate that the LSTM algorithm correctly identifies failures within dynamic operational windows.

<h3> Project Details </h3>

**Data Collection and Preprocessing:**
For this project, the data source is imported NASA sensor readings from mission-critical asset production. The sensor data was cleaned, normalized, and preprocessed to ensure data integrity. A sample of the visualized sensor data is shown below:
<br>

  ![image](https://github.com/zenjen-devs/zenjen-devs.github.io/assets/84609216/30ac2eb0-e2f6-4480-a3e7-e258b0bf476b)
  
Data Source: [NASA](https://data.nasa.gov)

<br><br>
**A Novel Approach to Feature Engineering:**
The benefit of applying deep learning in the predictive maintenance domain is that these networks can automatically extract the most impactful features from the data, eliminating the need for manual feature engineering. The idea of using LSTMs is to let the model extract abstract features out of the sequence of sensor values in the window, rather than engineering those manually. The expectation is that if there is a pattern in these sensor values within the window prior to failure, the pattern should be encoded by the LSTM.

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
     

*Precision = 0.97* <br>
When the LSTM model predicted an engine failure, it was correct 97% of the time.
<br>
<br>
*Recall = 0.91* <br>
The LSTM model correctly identified 91% of all engine failures.
<br>
<br>
*F1-Score = 0.94* <br>
Considering that our specific goal is high precision in predicting failures, false negatives are more costly than false positives.
<br>
<br>

**Real-time Monitoring System:**
To integrate the model into the production process, we will implement a real-time monitoring system that provisions immediate alerts when potential engine failures are predicted.

**Integration with Maintenance Protocols:**
Upon completion of model validation and system implementation, we collaborated with service engineering teams to integrate predictive results into maintenance schedules, enabling proactive servicing and part replacement. <br>

By leveraging deep learning with LSTM networks, this project contributes to the enhanced safety and operational efficiency of high-risk aircraft engine production environments. Early detection of anomalies and potential failures minimizes downtime, reduces operational risks, and reinforces the commitment to safety and reliability in the aerospace industry.

**References:** [See Repository](https://github.com/zenjen-dev/deep-learning_predicting-failures/blob/main/DeepLearning_PredictiveMaintenance.ipynb) 
