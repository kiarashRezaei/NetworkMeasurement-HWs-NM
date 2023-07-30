Sure! Below is the template for the README file based on the provided code:

# Network Measurements - Homeworks

## Table of Contents

- [Homework 1- Active Measurement](#Homework1-Active Measurement)
- [Homework 2- Website Fingerprinting](#Homework2-Website Fingerprinting)
- [Homework 3- HTTP Request Arrival Estimation](#Homework3-HTTPRequestArrivalEstimation)


## Homework 1- Active Measurement
(Geographical Analysis of Round-Trip Time (RTT) in Network Communication)


### General Approach
In this project, I conducted a geographical analysis of Round-Trip Time (RTT) in network communication. The main objective was to examine the relationship between RTT and the geographical distance between a source (virtual machine) and multiple destination servers located in different countries.

### Part 1: Data Collection and Preprocessing
1. Obtaining IP Addresses: I obtained the IP address of the virtual machine assigned to me from Google Cloud. Additionally, I selected multiple destination servers from different countries and stored their addresses in a CSV file. I then read the CSV file as a pandas dataframe.

2. Geographical Coordinates: I retrieved the latitude and longitude of both the source (virtual machine) and the destination servers by sending HTTP GET requests to the [ipapi.co](https://ipapi.co/) website API. This information allowed me to calculate the geographical distances between the source and each destination.

3. Sending SYN Packets and Measuring RTT: To measure the RTT, I sent TCP SYN packets from the source to each destination server. Using Scapy, I computed the average RTT for each destination based on their responses.

4. Data Visualization: I created a dataframe containing the target server names, their corresponding average RTT, and the geographical distance from the source. The data was sorted in increasing order based on distances, and a plot was generated to visualize the relationship between RTT and distances.

### Part 2: Linear Estimation of RTT
Using the Polyfit method from the NumPy library, I performed a least square error regression to obtain a linear estimation of RTT based on the geographical distance. The resulting linear function can be expressed as: RTT = slope * distance + intercept. This estimation provides insights into the impact of geographical distance on RTT.

### Note
Please note that the accuracy of the linear estimation might vary due to other factors influencing RTT, such as network congestion, bandwidth, and packet loss. Nonetheless, the analysis provides valuable insights into the correlation between RTT and geographical distances, demonstrating that distance is a crucial factor in network communication performance.


## Homework 2- Website Fingerprinting 
(Network Traffic Classification using KNN and Cumulative Traces)

This project focuses on network traffic classification using K-nearest neighbors (KNN) and cumulative traces. The main steps involved in the project are as follows:

**Main Part:**

1. Capturing the traffic: Network traffic is captured using TShark with filters to extract TCP traffic between different websites. The traffic is generated by sending 10 consecutive requests to each website on March 28th.

2. Feature Extraction: Statistical features are extracted for both flows and reverse flows. The features include the number of packets, total bytes, minimum/maximum/mean packet size, and minimum/maximum/mean inter-arrival time (IAT). A DataFrame is constructed to store the extracted features.

3. Constructing the Dataset: The DataFrame with statistical features is created to represent the dataset for classification.

4. Train-Test Split: The dataset is divided into a training set (70%) and a test set (30%).

5. KNN Classification: K-nearest neighbors (KNN) classification is performed on the training set with various values of K (1 to 14). The accuracy is calculated as the evaluation metric for each K value.

6. KNN Classification with a Different Test Set: A new test set is generated by capturing traffic on March 29th using 3 consecutive requests to each website. The same KNN classification is applied to the new test set using the same training set.

**Conclusion:** The performance in KNN classification decreased when using a new test set compared to the previous test set. This is likely due to the dynamic nature of news websites, resulting in daily changes in traffic patterns.

**Last Part:**

7. Cumulative Traces: A cumulative function of data packets in a network flow is computed. The cumulative traces are obtained based on the direction of the flow (uplink or downlink) and are used as features for classification.

8. Creating X_trace and Y_trace: The cumulative traces are generated for each flow, and the data is normalized. The cumulative traces data and corresponding website labels are used to create X_trace and Y_trace datasets.

9. KNN Classification and Performance Evaluation: KNN classification is performed on X_trace using the same process as in the main part. Accuracy is computed for each value of K (1 to 14), and confusion matrices are plotted for performance evaluation.

**Performance Comparison:** The performance of the cumulative traces approach is compared to the classical approach using the main dataset. Both approaches yield similar performance results.

Overall, this project demonstrates the application of KNN and cumulative traces in classifying network traffic and highlights the impact of dynamic traffic patterns on classification accuracy.


## Homework 3- HTTP Request Arrival Estimation
(Video Traffic Analysis)

This repository contains a Jupyter Notebook for video traffic analysis. The notebook aims to predict the arrival time of the next uplink (UL) request sent by a video client and the size of the response from the video server. The analysis is performed on a dataset of 21 video sessions.

### Tasks
The notebook covers the following tasks:

1. **Dataset Preparation**: The notebook uses a dataset of network traffic, filtering it to recognize the IP addresses of the video servers and selecting video traffic. If multiple servers are found, only the dominant flow is kept.

2. **Feature Extraction**: Various features are computed from the network traffic to be used for prediction. These features include:
   - Client Request Size (Uplink packets with size greater than or equal to 100 Bytes)
   - Inter Request-Response Time
   - Download Time, Download Volume, and Download Size (# Packets)
   - Playback Time

3. **Groundtruth Generation**: The groundtruth information is extracted from the dataset to be used for training the prediction models. The groundtruth includes the time for the next UL request and the size of the response from the server to that request.

4. **Regression Models**: Three regression models are used for prediction:
   - Random Forest
   - Support Vector Regression (SVR)
   - Multi Layer Perceptron (MLP)

### Results
The notebook compares the performance of the three regression models on the prediction task. The Random Forest model shows the closest results to the expected values.
