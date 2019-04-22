# Spark_Python_Anomaly_Detection_with_IBM_Waston
A simple anomaly detection of Internet of Things Sensor data for preventive maintenance purpose.
## Problem Framing
Nowdays all kinds of data have been creating everyday. The big Volume of the data, high Velocity of data and Varity types of data all demond advanced data analytics approach to better cater to the business needs. For example, when we build a real time data analytics platform for autonomous driving cars to deal with various data coming from camera, sensor, radar and lidar. The huge volume and velocity of the data both require we deploy the data analytics in high performance but low cost cloud computing enviroment. Especially, from the driving safty persepective, we need low latency and high throughout real time parallel data analytics system. In this case, suppose we have thousands of washing machines working at the same time in the different locations constaining a kind of Washing Machine Internet of Things or Internet of Washing Machines. We have different sensors to mintor and record the water flowrate, voltage, water fluid level,  frequency, hardness, spin speed, and water temperature. We care about the voltage, hardness and flowrate and proceed some basic analysis about this kind of data as sign of predicting the malfunction rate or preventive maintenance indicator and also for other downstream analysis purposes. So, we detect the outliers and plot them.

## Problem Solution
Using mainstream cloud computing services like AWS, Microfost Azure, IBM waston studio, GCP(Google Could Plotform) or Alibaba cloud. In this case we will choose IBM waston studio to build a simple Anomaly Detecton Argorthim for Washing Machine Sensor Data stored in Apache CouchDB in Cloud, specifically, we will detect the valtage data in range of 60 minutes of the Washing Machine Working time.

a simple anomaly sensor data detection using Spark Python with IBM Waston in IBM Cloud

## Setup 
1) Computer Operation System: Windows10 
2) Language:Python 3.5 With Spark 2.3
3) Libraries: Pyspark.sql, IBMos2Spark, Matplotlib

## Main Steps:
1) Connect to Apache CouchDB and Load sensor data from Apache CouchDB
2) Register the dataframe in the ApacheSparkSql catalog so that we can query it using SQL
3) Creat a python list of the Voltage data.
4) Visualize voltage data using a box plot to get an idea on the value distribution of this parameter.
5) Find out the date range and add 60 minutes as time dimension for analysis and visualization.
6) Primitive anomaly analysis conlusion
7) Double-Check the primitive conlusion by ploting a histogram which bins together certain voltage value ranges and counts the frequency of occurences of values within this range.

## Anomaly analysis conlusion
1) Most of the data points are lying around hardness 60-80, temperature 80-100 and flowrate 80-100.
2) There are some outliers, especially when it comes to the range of hardness 100-120.
3) Data follows some narrow boundaries.

## Thoughts and reflections
1) Be aware of using random sample function in order to obtain the random fraction of the original data properly. Image that the data frame could potentially contain trillions of rows and petabytes of data. There is no way to pass such an amount of data to a plotting library if the plotting code is always executed on a single machine.
**result.rdd.map(lambda row : row.voltage).sample(False,0.1).collect()**
2) Becareful of the Java Version. Trying to read a Parquet file in PySpark but getting Py4JJavaError. The spark-shell was using Java 1.8, but PySpark was using Java 10.1. There is some issue with Java 1.9/10 and Spark. Changed the default Java version to 1.8.

