# AWS Deployment Project: PySpark Word Count & Dockerized Node.js Web App

## Overview

This project consists of two tasks:

- **Task 1:** Perform word count using PySpark on a dataset stored in an S3 bucket, executed from an AWS Lightsail instance.
- **Task 2:** Create a Dockerized Node.js web server, push the image to Docker Hub, and deploy it on an AWS Lightsail instance.

---

## 📌 Important Links

- **Web App URL:** [http://3.89.209.39/](http://3.89.209.39/)
- **Docker Hub Repo:** [https://hub.docker.com/r/saiharsha027/node-webserver](https://hub.docker.com/r/saiharsha027/node-webserver)
- **GitHub Repo:** [https://github.com/saiharsha27/word-count-spark-hands-on-11](https://github.com/saiharsha27/word-count-spark-hands-on-11)

---

## Task 1: Word Count using PySpark on AWS Lightsail

### Steps

1. **Set up Lightsail instance** with Amazon Linux 2.
2. **Install dependencies**:
   ```bash
   sudo yum install java-11 python3-pip -y
   pip3 install pyspark
   ```
3. **Mount /tmp** and export JAVA_HOME:
   ```bash
   sudo mount -o remount,size=2G /tmp
   export JAVA_HOME=$(dirname $(dirname $(readlink -f $(which java))))
   ```
4. **Write and run `word_count.py`**, pointing to the S3 file:
   ```bash
   spark-submit word_count.py
   ```
5. **Output written to S3**, verify via AWS Console.

---

## Task 2: Node.js Web Server with Docker on AWS Lightsail

### Steps

1. **Set up a Node.js server** with Express.
2. **Create a `Dockerfile`** to containerize the app.
3. **Build and push Docker image** to Docker Hub:
   ```bash
   docker buildx create --use
   docker buildx build --platform linux/amd64 -t saiharsha027/node-webserver:latest --push .
   ```
4. **Deploy on Lightsail**:
   - Install Docker
   - Pull image from Docker Hub
   - Run container:
     ```bash
     docker run -d -p 80:3000 saiharsha027/node-webserver:latest
     ```
5. **Access app** via public IP at: [http://3.89.209.39/](http://3.89.209.39/)