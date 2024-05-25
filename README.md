# Practical Exercise 3: Data Processing and Mining in Big Data with Spark

## Introduction
In this practical exercise, we explore data processing and mining techniques for large datasets using Apache Spark. The goal is to solve a classification problem by developing various models, leveraging the Spark MLlib library, and comparing their performances. We use Docker to set up a scalable Spark cluster environment.

## Setup and Environment

### Docker Setup
We set up a Spark cluster using Docker, with a master node and three worker nodes. This setup ensures that our environment is consistent and scalable. The `docker-compose.yml` file configures the services, and a startup script manages the roles of the Spark instances.

### Steps to Set Up the Environment
1. **Build Docker Images**: Custom Docker images were created for the Spark master and worker nodes. These images include all necessary dependencies and configurations for Spark.
   ```
   docker build -t myspark-master:3.5.1 -f Dockerfile.master .
   docker build -t myspark:3.5.1 -f Dockerfile.worker .
   ```
   Master Image
   
   ![image](https://github.com/sml99/ccsa-p1/assets/29798184/ac4ad29f-c54d-4122-ba9f-44c0dc8f837c)
   
   Worker Image
   
   ![image](https://github.com/sml99/ccsa-p1/assets/29798184/a7e476aa-2d3a-455c-a3f5-4240a16f2324)

2. **Run the Cluster**: Using Docker Compose, we brought up the entire cluster. This command initializes the master and worker nodes, ensuring they are correctly configured and can communicate with each other.
   ```
   docker-compose up -d
   ```
   ![image](https://github.com/sml99/ccsa-p1/assets/29798184/c2ae4303-dcc6-42eb-aa54-932312bdcf00)
   ![image](https://github.com/sml99/ccsa-p1/assets/29798184/c74730cd-eaf2-4668-9b96-b9f581c3a2e6)

3. **Submit a Job**: A Flask application was set up to handle job submissions to the Spark cluster, allowing for efficient job management.
  ```
   docker exec -it practica3spark-spark-master-1 bash
   # running 
   ./bin/spark-submit /opt/spark-apps/celestial_ms.py --output /opt/spark-data/out --input /opt/spark-data/extra_small_celestial.csv
  ```
  ![image](https://github.com/sml99/ccsa-p1/assets/29798184/3132994f-8a51-4b6d-a762-b4ed3559757b)

- **Spark Master UI**:
![Spark Master UI](spark_master_ui.png)

## Data Preprocessing

### Data Loading
The dataset used for this exercise is `extra_small_celestial.csv`, located in the data directory. This dataset contains multiple features and a target variable, which we aim to predict.

### Preprocessing Steps
1. **Handle Missing Values**: We handled any missing values in the dataset to ensure data quality.
2. **Feature Scaling**: Features were scaled to standardize the data, which improves the performance of machine learning algorithms.
3. **Indexing the Target Variable**: The target variable was converted into a numerical format suitable for classification.

#### Screenshots:
- **Dataframe Loaded**:
![Dataframe Loaded](dataframe_loaded.png)
- **Preprocessed Data**:
![Preprocessed Data](preprocessed_data.png)

## Building and Evaluating Classifiers

### Classifiers Used
We implemented three classifiers using Spark's MLlib library:
1. Decision Tree Classifier
2. Random Forest Classifier
3. Logistic Regression

### Evaluation Metrics
Each classifier was evaluated using the accuracy metric. The dataset was split into training and testing sets to measure the performance of the models.

### Results
The accuracies of the classifiers on the test set are as follows:
- **Decision Tree**: Achieved an accuracy of X.X%.
- **Random Forest**: Achieved an accuracy of X.X%.
- **Logistic Regression**: Achieved an accuracy of X.X%.

*(Replace X.X% with actual results)*

#### Screenshots:
- **Decision Tree Results**:
![Decision Tree Results](decision_tree_results.png)
- **Random Forest Results**:
![Random Forest Results](random_forest_results.png)
- **Logistic Regression Results**:
![Logistic Regression Results](logistic_regression_results.png)

## Conclusion
In this exercise, we successfully set up a Spark cluster using Docker and built a Flask application for job submission. We preprocessed a large dataset, trained three different classifiers, and evaluated their performances. The Random Forest classifier achieved the highest accuracy, demonstrating its effectiveness in handling the classification task.

## Future Work
- **Hyperparameter Tuning**: Experimenting with hyperparameter tuning for each classifier could further improve accuracy.
- **Additional Preprocessing**: Exploring additional preprocessing techniques could enhance model performance.
- **Cross-Validation**: Implementing cross-validation would provide a more robust evaluation of model performance.

#### Screenshots:
- **Final Results Comparison**:
![Final Results Comparison](final_results_comparison.png)

## References
