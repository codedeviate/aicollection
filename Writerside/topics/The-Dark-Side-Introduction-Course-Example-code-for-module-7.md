# Example code for module 7

Below are several code examples that illustrate how emerging technologies—specifically AI and machine learning—can be integrated into penetration testing workflows. These examples demonstrate techniques for automated anomaly detection and vulnerability prioritization. They are intended for educational purposes and should be run only in controlled, authorized environments.

---

## Example 1: Anomaly Detection with Isolation Forest

This Python script uses scikit-learn’s Isolation Forest algorithm to analyze synthetic network traffic data and detect anomalies. In a real-world scenario, similar techniques can help identify subtle indicators of compromise that might otherwise be overlooked by manual analysis.

> **Prerequisites:**  
> Install required packages with:
> ```bash
> pip install numpy pandas scikit-learn matplotlib
> ```

```python
# anomaly_detection.py
import numpy as np
import pandas as pd
from sklearn.ensemble import IsolationForest
import matplotlib.pyplot as plt

# Generate synthetic network traffic data
np.random.seed(42)
# Simulate normal traffic (clustered around [20,20])
normal_data = 0.3 * np.random.randn(100, 2) + np.array([20, 20])
# Inject anomalies (unusual points)
anomalies = np.random.uniform(low=15, high=25, size=(10, 2))
data = np.vstack((normal_data, anomalies))
df = pd.DataFrame(data, columns=["feature1", "feature2"])

# Train IsolationForest for anomaly detection
model = IsolationForest(contamination=0.1, random_state=42)
df["anomaly"] = model.fit_predict(df[["feature1", "feature2"]])

# Plot the results
plt.figure(figsize=(8, 6))
plt.scatter(df["feature1"], df["feature2"], c=df["anomaly"], cmap='coolwarm', edgecolor='k')
plt.xlabel("Feature 1")
plt.ylabel("Feature 2")
plt.title("Anomaly Detection with Isolation Forest")
plt.show()

# Print out detected anomalies
print("Anomalies detected:")
print(df[df["anomaly"] == -1])
```

*What It Does:*
- Generates synthetic data representing network traffic.
- Trains an Isolation Forest model to learn the normal behavior.
- Flags and visualizes data points that deviate significantly from the norm as anomalies.

---

## Example 2: Automated Vulnerability Prioritization with Random Forest

This script simulates an ML-based approach for prioritizing vulnerabilities. A Random Forest classifier is trained on a synthetic dataset of vulnerability features (e.g., vulnerability score, exploitability, impact) to classify whether a vulnerability is high risk. In practice, such models can help security teams focus remediation efforts on the most critical issues.

> **Prerequisites:**  
> Install required packages with:
> ```bash
> pip install numpy pandas scikit-learn
> ```

```python
# vulnerability_prioritization.py
import numpy as np
import pandas as pd
from sklearn.ensemble import RandomForestClassifier
from sklearn.model_selection import train_test_split
from sklearn.metrics import classification_report

# Create a synthetic vulnerability dataset
data = {
    "vulnerability_score": np.random.randint(1, 10, 100),
    "exploitability": np.random.randint(1, 5, 100),
    "impact": np.random.randint(1, 10, 100)
}
df = pd.DataFrame(data)

# Define a risk metric and create a binary target (1 = high risk, 0 = low risk)
df["risk_metric"] = (df["vulnerability_score"] * df["impact"]) / df["exploitability"]
threshold = df["risk_metric"].median()
df["high_risk"] = (df["risk_metric"] > threshold).astype(int)

# Prepare features and target
X = df[["vulnerability_score", "exploitability", "impact"]]
y = df["high_risk"]

# Split dataset into training and testing sets
X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.2, random_state=42)

# Train a Random Forest Classifier
clf = RandomForestClassifier(n_estimators=50, random_state=42)
clf.fit(X_train, y_train)

# Evaluate the model on the test set
predictions = clf.predict(X_test)
print("Classification Report:\n")
print(classification_report(y_test, predictions))

# Simulate predictions on new vulnerability data
new_data = pd.DataFrame({
    "vulnerability_score": [7, 3, 9],
    "exploitability": [2, 4, 1],
    "impact": [8, 5, 10]
})
new_predictions = clf.predict(new_data)
new_data["predicted_high_risk"] = new_predictions
print("\nNew Vulnerability Predictions:")
print(new_data)
```

*What It Does:*
- Generates a synthetic dataset with features representing vulnerability characteristics.
- Calculates a risk metric and labels data as high or low risk.
- Trains a Random Forest classifier to predict the risk category.
- Evaluates the model and simulates predictions on new vulnerability samples.

---

## Final Notes

These examples illustrate how AI and ML can enhance penetration testing by:
- **Automating Routine Tasks:** Reducing manual workload and quickly processing large datasets.
- **Detecting Anomalies:** Flagging unusual patterns in network traffic that may indicate emerging threats.
- **Prioritizing Vulnerabilities:** Helping security teams focus on high-risk issues with data-driven insights.

By integrating these emerging technologies into your testing toolkit, you can improve both the efficiency and effectiveness of your cybersecurity assessments. As always, ensure that all testing is conducted ethically and legally, within controlled and authorized environments.

Happy learning, and stay adaptive in the ever-evolving landscape of cybersecurity!