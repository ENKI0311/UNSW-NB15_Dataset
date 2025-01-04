# Network Intrusion Detection System (NIDS) using Machine Learning

## Introduction
This project showcases a machine learning-based approach to detecting potential threats in network traffic data, focusing specifically on developing a **Network Intrusion Detection System (NIDS)**. Cybersecurity is a growing concern with the rapid expansion of digital networks, and being able to identify intrusions early is key to protecting sensitive data. By leveraging advanced machine learning models, we aim to build an efficient and effective system capable of distinguishing between benign and malicious network activities.

The dataset used for this project represents network traffic data, with various features like packet counts, bytes transferred, and connection durations. The objective is to train a model that can effectively predict whether a given network session is normal or suspicious. This system could be integrated into real-world cybersecurity setups to detect potential intrusions before they lead to breaches.

## Dataset Overview
The dataset comprises multiple features representing different aspects of network traffic. Key features include:
- **`dur` (Duration)**: The duration of the connection, which can help identify unusual activity, like very long or very short connections, often seen during Denial of Service (DoS) attacks.
- **`sbytes` and `dbytes` (Source and Destination Bytes)**: These represent the amount of data sent and received, which can indicate abnormal data flow, such as data exfiltration attempts.
- **`spkts` and `dpkts` (Source and Destination Packets)**: The number of packets sent and received during a connection. Large discrepancies between sent and received packets may suggest suspicious behaviors.

The dataset also includes several other features, which were subjected to detailed **exploratory data analysis (EDA)** to uncover patterns and relationships crucial for effective modeling. We employed **Principal Component Analysis (PCA)** to reduce the dimensionality while retaining most of the information, resulting in an optimal feature set for the classification models.

## Machine Learning Approach
### Feature Engineering
Feature engineering played a significant role in this project. We began by cleaning the data and handling missing values, followed by feature reduction to remove redundancy and eliminate multicollinearity. **Principal Component Analysis (PCA)** helped in reducing the dimensionality while retaining over 95% of the variance, ensuring that the reduced dataset remained informative for the models.

Key engineered features included:
- **Byte and Packet Ratios**: Calculated ratios between source and destination packets/bytes to better capture asymmetric network activity, which is common in attack scenarios.
- **Interaction Features**: Derived new features that represent interactions between key network metrics, helping to further enhance the ability to differentiate between normal and abnormal activity.

### Model Training
Several models were trained, including **Logistic Regression**, **Random Forest Classifier**, and **Support Vector Machine (SVM)**. The **Random Forest Classifier** emerged as the best performer, achieving near-perfect accuracy, precision, recall, and F1 scores even during cross-validation. This strong performance indicates that the Random Forest model is capable of capturing complex non-linear relationships in the data, making it highly effective for intrusion detection.

### Evaluation
The model evaluation focused on the implications of **precision, recall, and F1 scores** in a cybersecurity context:
- **High Precision**: Ensures fewer false alarms, which is critical to reducing alert fatigue for security teams.
- **High Recall**: Ensures that all potential threats are detected, which is crucial in minimizing the risk of missing an actual attack.
- **F1 Score**: Balances precision and recall, offering a comprehensive measure of model performance.

The Random Forest model achieved nearly perfect scores across all metrics, showcasing its suitability for real-world cybersecurity applications.

## Deployment
To demonstrate practical utility, we deployed the trained **Random Forest Classifier** as a **Flask API**. The API can receive input data representing network traffic features and return a prediction, indicating whether the activity is normal or malicious. This API can be integrated into a larger **Security Information and Event Management (SIEM)** system, providing a crucial automated layer in a broader network defense strategy.

A sample API endpoint allows users to make real-time predictions:
- **Endpoint**: `/predict`
- **Input**: JSON with the network traffic features.
- **Output**: JSON with the prediction result (`0` for normal, `1` for malicious).

## Future Work
This project serves as a foundational demonstration of how machine learning can bolster cybersecurity efforts. Future enhancements could include:
- **Unsupervised Anomaly Detection**: Integrate an unsupervised model to identify unknown attack types without pre-labeled data.
- **Real-Time Stream Processing**: Develop streaming capabilities to enable real-time classification of network packets.
- **Enhanced API Security**: Implement user authentication and rate limiting for the API to make it more secure for deployment.

## Conclusion
The machine learning-based Network Intrusion Detection System developed in this project offers a powerful way to detect and respond to network threats. With its emphasis on high recall and accuracy, the model has the potential to serve as an effective tool in a security professional's toolkit, providing timely alerts and reducing the likelihood of successful intrusions. The integration of a Flask API further demonstrates the system's readiness for real-time deployment in actual cybersecurity environments.

## Getting Started
### Prerequisites
- **Python 3.7+**
- **Flask**
- **Scikit-learn**
- **Joblib**

### Installation
1. Clone the repository:
   ```bash
   git clone https://github.com/ENKI0311/nids-ml-project.git
   ```
2. Install the required dependencies:
   ```bash
   pip install -r requirements.txt
   ```
3. Run the Flask API:
   ```bash
   python model_api.py
   ```

## Usage
After starting the API, you can send POST requests to the `/predict` endpoint with JSON data containing the network traffic features to get a classification result.

```python
import requests

url = 'http://127.0.0.1:5000/predict'
input_data = {
    'features': [0.5, -0.2, 0.3, 1.0, -0.1]  # Example input representing 5 principal components
}
response = requests.post(url, json=input_data)
print(response.json())
```

## License
This project is licensed under the MIT License.

