# 🌐 Python App Deployment on AWS Elastic Beanstalk.
The Techaj Python Logging App is a lightweight web application deployed on AWS Elastic Beanstalk. It demonstrates how to use a Python WSGI app with structured logging, IAM roles, and S3-based deployment. The app responds with a custom HTML page and logs incoming POST requests, making it ideal for learning cloud deployment basics with real-world scenarios.

## 📦 Prerequisites ✅

Before starting, ensure you have:

- 🔹 An **AWS account**   
- 🔹 Code packaged in a **ZIP file**   
- 🔹 A **Python application** ready for deployment 
- 🔹 ✅ IAM permissions to create roles, EC2, and Elastic Beanstalk apps  
- 🔹 🧠 Basic understanding of Python and web apps  

---

## 🎯 Learning Objectives

By the end of this project, you will:

- ✅ Deploy a Python web app using **Elastic Beanstalk**  
- ✅ Create and assign an **IAM instance profile role**  
- ✅ Serve a custom **HTML response with logging**  
- ✅ Use **S3** as the app source for Elastic Beanstalk  
- ✅ Access the app via a public **domain URL**

---

## 🪜 Step-by-Step Deployment Guide

### 1️⃣ Log In to AWS Console

- 🔐 Visit [https://aws.amazon.com](https://aws.amazon.com)  
- 👤 Sign in with your root or IAM user account  

---

### 2️⃣ Open IAM & Create an Instance Profile Role 🔐

_ IAM Role is required for Elastic Beanstalk to manage EC2 and other services._

- Go to **IAM → Roles → Create Role**  
  - Select **Trusted entity**: AWS service  
  - Use case: **Elastic Beanstalk**  
- Attach these policies:
  - `AWSElasticBeanstalkWebTier`  
  - `AWSElasticBeanstalkMulticontainerDocker`  
  - `AWSElasticBeanstalkWorkerTier`  
  - `AmazonS3FullAccess`   
- Name the role: `Instance-profile-EBS-role`  
- ✅ Click **Create role**  

![IAM-Role](https://github.com/iam-avinash-jagtap/Web-Application-Deployment-Using-AWS-Elastic-BeanStalk/blob/master/Images/Screenshot%202025-04-30%20180234.png)

---

### 3️⃣ Open Elastic Beanstalk Console 🌿

- Navigate to **Services → Elastic Beanstalk**  
- Click **Create application**  

---

### 4️⃣ Create Your Application 📦

- **Application name**: `PythonApp`  
- Description: This is Flask app Deployment using Elastic BeanStalk  
- Click **Next** to configure the environment  

---

### 5️⃣ Create an Environment 🛠️

- Choose **Environment tier**: `Web server environment`  
- Platform:  
  - Select **Python**  
  - Platform branch: Latest supported version (e.g., Python 3.8/3.9)  
- **Application code**:  
  - ✅ Choose **Upload your code**  
  - Upload your **ZIP file**  
  - Or select **Get code from S3**:
    - Upload your ZIP to an **S3 Bucket** 
  
![S3-Bucket](https://github.com/iam-avinash-jagtap/Web-Application-Deployment-Using-AWS-Elastic-BeanStalk/blob/master/Images/Screenshot%202025-04-30%20180600.png)

  - Paste the full **S3 URI**  
- Instance settings:
  - Environment name: `Python-App-Env`  
  - Domain: auto-generated (e.g., `python-app-env.eba-xyz123.elasticbeanstalk.com`)  
  - ✅ Select **Single instance**  

---

### 6️⃣ Configure More Options ⚙️

- Under **Configure more options**:
  - **Instances**:
    - Instance type: `t2.micro` 
    - IAM instance profile: `Instance-profile-EBS-role`  
  - **Software**:
    - Add environment variables if needed  
  - **Logs**:
    - Enable log streaming or retention to S3  

- ✅ Click **Create environment**

---

### 7️⃣ Launch Your Environment 🚀

Elastic Beanstalk will now:

- Launch an EC2 instance  
- Install Python  
- Deploy your app  
- Set up networking and URL  

You’ll see:

- 🎉 Health: **Green**  
- 🌐 Domain: `http://python-app-env.eba-xyz123.elasticbeanstalk.com`  

![ENV](https://github.com/iam-avinash-jagtap/Web-Application-Deployment-Using-AWS-Elastic-BeanStalk/blob/master/Images/Screenshot%202025-04-30%20180726.png)

---

### 8️⃣ Test Your Application 🧪

- Visit the app’s domain URL  
- You should see your **Techaj-branded HTML page**  

![Output](https://github.com/iam-avinash-jagtap/Web-Application-Deployment-Using-AWS-Elastic-BeanStalk/blob/master/Images/Screenshot%202025-04-30%20180045.png)

- POST requests to `/` and `/scheduled` will trigger logging  
- Logs are stored at `/tmp/sample-app.log` on the EC2 instance  

---
### 9️⃣ (Optional) Use Auto Scaling Group for High Availability

Select “Load Balanced + Auto Scaling” instead of a single instance during environment creation.

This ensures better uptime, automatic instance recovery, and efficient traffic distribution for production-ready apps.
---
## Summary
This project, Techaj Python Logging App, showcases the deployment of a simple Python WSGI web application on AWS Elastic Beanstalk. It includes structured logging using Python's RotatingFileHandler and serves a custom HTML response on the root path. The app handles POST requests for logging and simulates task scheduling with log capture. IAM instance profile roles are configured to securely allow Elastic Beanstalk access to EC2 and other resources. The application is deployed via a ZIP file or S3 bucket, runs on a single EC2 instance, and is accessible through a public Elastic Beanstalk domain. This project serves as a practical guide to deploying and managing Python apps on AWS.
