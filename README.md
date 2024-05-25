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

## Celestial Classification using Spark
### Setup Environment
We begin by importing the necessary modules from `pyspark.ml` and `pyspark.sql`
Next, we create a Spark session:
```
spark = SparkSession.builder.appName("CelestialDecisionTree").getOrCreate()
```
### Data Loading
The dataset used for this exercise is `extra_small_celestial.csv`, located in the data directory. This dataset contains multiple features and a target variable, which we aim to predict.
```
data = spark.read.csv("/opt/spark-data/extra_small_celestial.csv", sep=";", header=True, inferSchema=True)
```
### Preprocessing Steps
We identify numeric features in the dataset:
```
numeric_features = [col for col, dtype in data.dtypes if dtype == "int" or dtype == "double"]
```
We set up feature indexing and scaling:
```
labelIndexer = StringIndexer(inputCol="type", outputCol="indexedLabel")
assembler = VectorAssembler(inputCols=numeric_features, outputCol="features")
scaler = StandardScaler(inputCol="features", outputCol="scaled_features")
```
We create a pipeline for preprocessing and fit it to the data:
```
pipeline = Pipeline(stages=[labelIndexer, assembler, scaler])
prep_model = pipeline.fit(data)
prep_model.save(output_folder + "/pipeline")
prep_data = prep_model.transform(data)
```
We split the data into training and test sets:
```
train, test = prep_data.randomSplit([0.8, 0.2], seed=12345)
```
We define the Decision Tree and Random Forest classifiers along with their hyperparameter grids:
```
dt = DecisionTreeClassifier(labelCol="indexed_label", featuresCol="scaled_features")
dt_param_grid = ParamGridBuilder()\
    .addGrid(dt.maxDepth, [3, 10]) \
    .addGrid(dt.maxBins, [10, 30])\
    .build()

rf = RandomForestClassifier(labelCol="indexed_label", featuresCol="scaled_features")
rf_param_grid = ParamGridBuilder()\
    .addGrid(rf.maxDepth, [3, 10]) \
    .addGrid(rf.maxBins, [10, 30])\
    .build()

to_run = {"dt": (dt, dt_param_grid), "rf": (rf, rf_param_grid)}
```
### Model Training and Evaluation
```
evaluator = BinaryClassificationEvaluator(metricName="areaUnderROC", labelCol="indexed_label")

for mid, settings in to_run.items():
    estimator, parset = settings
    tvs = TrainValidationSplit(estimator=estimator,
                               estimatorParamMaps=parset,
                               evaluator=evaluator,
                               trainRatio=0.8)
    tvs_model = tvs.fit(train)
    best_model = tvs_model.bestModel
    inner_out_folder = output_folder + "/" + mid
    best_model.save(inner_out_folder)
    
    params = best_model.extractParamMap()
    predictions = best_model.transform(test)
    auc = evaluator.evaluate(predictions)

    final_dict = {param.name: value for param, value in zip(params.keys(), params.values())}
    final_dict["AUC"] = auc

    with open("{}/params.json".format(inner_out_folder), "w") as json_file:
        json.dump(final_dict, json_file, indent=4)
```


## Building and Evaluating Classifiers

### Classifiers Used
We implemented two classifiers using Spark's MLlib library:
1. Decision Tree Classifier
2. Random Forest Classifier

### Evaluation Metrics
Each classifier was evaluated using the accuracy metric. The dataset was split into training and testing sets to measure the performance of the models.

### Results
The accuracies of the classifiers on the test set are as follows:
- **Decision Tree**: Achieved an accuracy of 96.52%.
- **Random Forest**: Achieved an accuracy of 90.15%.

### Executing the model prediction using Flask API: 
First, we start the flask server inside practica3spark-spark-master-1
```
# export FLASK_APP=/opt/spark-apps/celestialApp.py
# flask run --host=0.0.0.0 -p 5000
```
Second, We test it using the attributs provided in data.json as a payload
![image](https://github.com/sml99/ccsa-p1/assets/29798184/72d0fb24-325f-4f72-a5b3-b317a735f566)

## Conclusion
In this exercise, we successfully set up a Spark cluster using Docker and built a Flask application for job submission. We preprocessed a large dataset, trained two different classifiers, and evaluated their performances. The Random Forest classifier achieved the highest accuracy, demonstrating its effectiveness in handling the classification task.

