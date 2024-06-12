# EECS 221 Final Report
## Table of Contents
1. [Introduction](#1-introduction)
2. [Motivation](#2-motivation)
3. [Problem Definition](#3-problem-definition)
4. [Technical Approach](#4-technical-approach)
5. [Evaluation](#5-evaluation)
6. [Discussion](#6-discussion)
7. [Future Works](#7-future-works)

## Information
### Team members
**Group 4 Members:** Mengting Yang, Tianzhou Gao, Xuzhong Chen, Ang Li
### *Work distribution:*
**Mengting Yang:** Experiment design, data collection, Unity development support, documentation.

**Tianzhou Gao:** Unity application development, webpage and code maintainance.

**Xuzhong Chen:** Machine Learning model training, IoT platform deployment, security analysis.

**Ang Li:** Experiment design, data collection, webpage and IoT deployment support, documentation.

### GitHub Link:
https://github.com/gtz123456/EECS221


## Abstract
This report presents the development and evaluation of a user identification system for the Hololens 2, leveraging AWS cloud services and machine learning models. The system collects and analyzes head and hand movement data to automatically identify user information, enhancing the security and personalization of Mixed Reality (MR) applications. Our approach addresses the challenges of accurate and reliable user identification in MR environments, where traditional methods may fall short due to the dynamic and immersive nature of the interactions. Through a combination of robust data collection, advanced machine learning techniques, and cloud-based processing, our system demonstrates significant improvements in user identification accuracy. The results of our evaluation indicate that the proposed system not only meets but exceeds the current standards, paving the way for more secure and customized MR experiences.

## 1. Introduction
The integration of Mixed Reality (MR) technology in various applications has opened up new possibilities for immersive user experiences. However, the increasing complexity of MR systems poses significant challenges in terms of user identification and data privacy. This project focuses on developing a robust MR application that leverages biometric data for seamless user identification while ensuring data privacy and security on Hololens. By offloading complex computations to cloud services, the system aims to provide a scalable and efficient solution that can be deployed across various hardware platforms.

## 2. Motivation
The demand for secure and personalized MR experiences is rapidly growing. Users expect a seamless interaction within shared MR environments, which reduces the trouble of explicitly entering ID or password. Existing research has shown that the integration of biometric data such as eye gaze, head position, and hand gestures can serve as powerful indicators of user identities. However, the data containing user identity information is sensitive and thus needs to be protected. Furthermore, leveraging cloud-based infrastructure for processing and storage ensures scalability and reduces the computational burden on local devices.

Based on the above needs, existing work, and infrastructure, our project focuses on developing a comprehensive method that employs certain biometric data of users while preserving user privacy with the help of cloud-based infrastructure.

## 3. Problem Definition
Identifying users accurately based on biometric data in MR applications presents several challenges. Specifically, the problem can be broken down into the following sub problems:

- **Accurate User Identification:** Differentiating between users based on their biometric data through ML is complex due to the variability in data patterns. Appropriate features need to be selected and the ML model needs to be effective and concise in the meantime to support online application. 

- **Data Privacy and Security:** Ensuring that user data is securely transmitted and stored is crucial to prevent unauthorized access and breaches. A threat model needs to be developed with all possible ways of malicious data access identified. After that light-weighted encryption algorithms ought to be deployed to protect the malicious access. 

- **Real-time Processing:** Balancing the complexity of the identification model with the need for real-time processing is essential to maintain a seamless user experience.

## 4. Technical Approach
### Unity MR Application Development
The development of the MR application was conducted using **Unity**, a widely-used game development platform. The **Microsoft Mixed Reality Toolkit (MRTK)** and the **hl2ss** plugin were utilized to facilitate the integration of various sensors with the **Hololens 2** device.

#### Development Environment:

- [Hololens 2:](https://www.microsoft.com/en/hololens) A mixed reality headset that provides an immersive experience through advanced sensors and computational capabilities.
- [Unity:](https://unity.com/) A versatile development platform used for creating interactive applications.
- [Microsoft Mixed Reality Toolkit (MRTK):](https://learn.microsoft.com/en-us/windows/mixed-reality/mrtk-unity/mrtk2/?view=mrtkunity-2022-05) A collection of tools that simplifies the development of MR applications.
- [hl2ss Plugin:](https://github.com/jdibenes/hl2ss) Facilitates the integration of sensors with the Hololens 2.

#### Sensors Used:

- Head Angle Sensor: Captures the orientation of the user’s head.
- Eye Tracking Sensor: Tracks the user's eye movements.
- Forehead Cameras: Used for hand tracking to capture hand gestures.

#### Application Workflow:

The MR application workflow involves the creation of virtual objects that users interact with by dragging them to their identical pairs. During this interaction, data related to **eye gaze**, **head position**, and **hand gestures** are collected and sent to AWS services for processing. This workflow ensures the collection of rich biometric data necessary for user identification.

### Experiment and Data Collection
#### Experiment Design:

The experiment was designed to collect data from a diverse group of participants to ensure variability in the biometric data. Eight students from UCI, with different shapes, ages, and genders, participated in the study. Each subject used the MR application for a trial period of three minutes, repeated multiple times.

#### Data Collected:

The primary data collected included **raw head pose**, **wrist pose**, and **eye gaze** data. This data was captured using the hl2ss plugin and stored for further processing and model training.

#### ML Model Training
- **Model Selection:**
The ***multiclass_estimator*** model was chosen for its balance between efficiency and accuracy. This model had previously demonstrated superior performance compared to other models evaluated in preliminary studies.
  
-  **Process:** The training process involved collecting pre-training data from all group members, focusing initially on head position data. This pre-training data was used to build a foundational model, which was subsequently enhanced using newly collected data from the experiments.

- **Deployment and Validation:** The trained model was deployed on **AWS Sagemaker**, a cloud-based machine learning service. Validation of the model was conducted using data from the team members, achieving an accuracy of approximately 80%. This validation process ensured the model’s robustness and readiness for deployment.

### Cloud Service
#### Reduced Device Load:

Offloading complex computational tasks to the cloud significantly reduced the burden on the Hololens device. This approach allowed the MR application to run smoothly without the constraints of local computational resources.

#### Cross-Platform Compatibility:

Cloud-based inference supports various devices, including smartphones, tablets, and computers. This compatibility enhances the portability of the MR application, enabling access to cloud models via the internet.

#### Sufficient Computing Resources:

Cloud platforms provide powerful computing resources capable of handling complex machine learning models. This ensures faster inference results and avoids performance bottlenecks associated with limited local device resources.

#### AWS Services
Services Used:

- **IoT Platform:** Facilitates communication, data processing, and storage on the cloud.
- **Sagemaker:** Provides on-cloud ML model training and deployment services.
- **S3 Bucket:** Used for storing data on the cloud.
- **Lambda:** Enables on-cloud scripting for data processing and formatting.
- **API Gateway:** Serves as a connection hub for Hololens, local PC monitoring, and other AWS services.

## Encryption and Threat Model
Threats Addressed:

- **Client Attack:** The Hololens runs a single process OS, making it difficult for malware to collect data locally.
- **Client-to-Cloud Attack:** Data streaming is protected by HTTPS, and the raw data is hard to use without the correct cloud tags.
- **Cloud Attack:** AWS IAM authentication controls access, making it difficult for attackers to access data.
- **Cloud-to-Client Attack:** User tags are encrypted with MD5 and transmitted under HTTPS.

## 5. Evaluation
### Results
The evaluation of the MR application focused on three key areas: performance, security, and scalability.

#### Performance:

- **Accuracy:** The ML model achieved an accuracy of approximately 80%.
- **Latency:** The system operated in real-time with a latency of less than one second.
- **Efficiency:** The ML model was highly efficient, ensuring seamless user interactions.
- **Security:**
The threat model was thoroughly evaluated to ensure data protection at various stages.
Multiple encryption methods were implemented to safeguard data during transmission and storage.
- **Scalability:**
The use of AWS cloud services facilitated easy deployment across different hardware platforms.
The cloud-based approach ensured that the application could scale to accommodate a growing number of users and data.

## 6. Discussion
### Challenges
The development and deployment of the MR application presented several challenges:

1. **Hololens Hardware Limitations:** The performance of the Hololens hardware limited the sampling methods and rates. Additionally, the device does not support background applications, which constrained certain functionalities.
2. **Limited Sample Size:** The small sample size used for data collection reduced the overall accuracy of the ML model. A larger dataset is necessary to improve model performance.
3. **Encryption Deployment:** Implementing encryption algorithms on the Hololens was challenging due to limited hardware resources. Ensuring robust data encryption without compromising performance required careful balancing.

## 7. Future Works
The project identified several areas for future improvement and development:

1. **Model Refinement:** Further refinement of the ML models is needed to enhance accuracy and robustness. This includes exploring advanced algorithms and techniques to better handle the variability in biometric data.
2. **Expanded Data Sources:** Incorporating additional biometric data, such as detailed eye tracking and hand gestures, can provide a richer dataset for more accurate user identification.
3. **Real-world Deployment:** Testing the system in diverse and real-world scenarios is crucial to ensure its reliability and performance. This includes deploying the application in various environments and with a larger user base to gather comprehensive feedback.
