Main Application Documentation
Overview
The main application serves as the central control for bearing condition analysis, integrating functionalities from the library (intelliMaint_core.py) and the domain-specific module (bearing.py). It facilitates data acquisition, feature extraction, health scoring, anomaly detection, and diagnostics, providing an end-to-end solution for monitoring and diagnosing bearing conditions.
Key Steps:
•	- **Data Acquisition**: Loads signal data for analysis.
- **Feature Extraction**: Computes statistical and frequency-domain features.
- **Health Scoring**: Evaluates bearing health using clustering and anomaly detection.
- **Anomaly Detection**: Identifies fault onset and progression.
- **Diagnostics**: Analyzes fault modes and evaluates diagnostic features.
Function/Class Descriptions
Data Acquisition
Purpose: Loads and formats raw signal data from specified files.
Example:
data_dir_path = 'path_to_data'
data_acquisition = DataAcquisition()
files = data_acquisition.get_file_list(data_dir_path)
print(f'Total files found: {len(files)}')
Feature Extraction
Purpose: Extracts time-domain and frequency-domain features using the Bearing class.
Example:
bearing = Bearing(files)
signal = pd.to_numeric(df['column'], errors='coerce').dropna().values
features = bearing.extract_features(signal)
print(features)
Health Scoring
Purpose: Uses SOM for clustering features and evaluates health scores.
Example:
som = SOM()
trained_som, scaler = som.train(train_data)
mqe = som.predict(trained_som, test_data, scaler)
plt.plot(mqe)
Anomaly Detection
Purpose: Detects anomalies and identifies the start of fault progression.
Example:
anomaly_detection = AnomalyDetection()
anomaly_detection.train_cosmo(train_data)
health_scores, _ = anomaly_detection.test_cosmo(test_data)
plt.plot(health_scores)
Diagnostics
Purpose: Evaluates and visualizes diagnostic features for fault classification.
Example:
diagnostics = Diagnostic()
diagnostic_features = diagnostics.evaluate_diagnostic_features(df_features, labels)
diagnostics.plot_diagnostic_features(diagnostic_features, top_n=5)
Workflow Integration
The main application integrates functionalities from the library and domain-specific modules to provide a seamless workflow from data acquisition to diagnostics. Below is a high-level overview:
•	- The `DataAcquisition` class retrieves signal files and processes raw data.
- The `Bearing` class extracts features for analysis.
- The `SOM` and `AnomalyDetection` classes compute health scores and detect anomalies.
- The `Diagnostic` class evaluates fault modes and identifies critical features.
Flowchart
The flowchart below illustrates the dependencies and overall workflow from data acquisition to diagnostics.

