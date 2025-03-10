# **📌 Real-Time Stock Market Data Pipeline Using Kafka & AWS**  

## **🚀 Overview**  
This project builds a **real-time stock market data pipeline** using **Apache Kafka, AWS S3, AWS Glue, and Amazon Athena** to simulate stock price movements, ingest streaming data, and enable real-time analytics.  

🔹 **Kafka Producer** streams simulated stock data.  
🔹 **Kafka Broker (EC2)** handles real-time data ingestion.  
🔹 **Kafka Consumer** processes data and stores it in **Amazon S3**.  
🔹 **AWS Glue Crawler** detects schema and updates the **Glue Data Catalog**.  
🔹 **Amazon Athena** enables **SQL queries** on stock market data.  

---

## **🛠 Tech Stack**  
- **Programming Language**: Python (Boto3, Kafka-python, Pandas)  
- **Messaging System**: Apache Kafka (Hosted on AWS EC2)  
- **Cloud Storage**: Amazon S3  
- **ETL & Schema Detection**: AWS Glue & Glue Data Catalog  
- **Query Engine**: Amazon Athena  
- **Infrastructure**: AWS IAM, AWS EC2, AWS Glue, AWS Athena  

---

## **📌 Architecture Overview**  



1️⃣ **Kafka Producer** simulates real-time stock prices from a dataset and sends messages to Kafka.  
2️⃣ **Kafka Broker (on EC2)** handles real-time message ingestion.  
3️⃣ **Kafka Consumer** processes stock data and writes structured data to **Amazon S3**.  
4️⃣ **AWS Glue Crawler** scans the raw data and updates the **Glue Data Catalog**.  
5️⃣ **Amazon Athena** enables SQL-based analysis directly on S3 data.  

---

## **📂 Project Structure**  
```
├── producer.py             # Kafka producer for simulating stock market data
├── consumer.py             # Kafka consumer for processing data
├── config.py               # Configuration for Kafka, AWS keys, S3 bucket
├── setup_kafka.sh          # Kafka setup script for AWS EC2
├── README.md               # Project documentation
└── dataset/                # Sample stock market dataset (CSV)
```

---

## **🚀 Setup & Installation**  

### **1️⃣ Prerequisites**  
✔ **AWS Account** (Free Tier)  
✔ **EC2 Instance (Ubuntu/Amazon Linux)** for hosting Kafka  
✔ **IAM Role** with S3, Glue, and Athena permissions  
✔ **Python 3.x** and required dependencies  

### **2️⃣ Clone Repository & Install Dependencies**  
```bash
git clone https://github.com/your-repo/kafka-stock-market-pipeline.git
cd kafka-stock-market-pipeline
pip install -r requirements.txt
```

### **3️⃣ Set Up Kafka on AWS EC2**  
```bash
chmod +x setup_kafka.sh
./setup_kafka.sh
```

### **4️⃣ Start Kafka Broker & Zookeeper**  
```bash
bin/zookeeper-server-start.sh config/zookeeper.properties
bin/kafka-server-start.sh config/server.properties
```

### **5️⃣ Run the Kafka Producer & Consumer**  
**Start the producer to send stock market data:**  
```bash
python producer.py
```
**Start the consumer to process & store data in S3:**  
```bash
python consumer.py
```

---

## **📌 AWS Setup**  

### **🛠 Create an S3 Bucket for Storing Data**  
1️⃣ Go to **AWS S3** → **Create Bucket** → Name it `kafka-stock-market-data`.  
2️⃣ Enable public access for testing (or set IAM policies for secure access).  

### **🛠 Set Up AWS Glue Crawler**  
1️⃣ Navigate to **AWS Glue** → **Crawlers** → **Create Crawler**.  
2️⃣ Choose S3 as the data source and select `kafka-stock-market-data`.  
3️⃣ Set up an IAM role with `AmazonS3FullAccess` & `AWSGlueServiceRole`.  
4️⃣ Run the Glue Crawler to create a **Glue Data Catalog Table**.  

### **🛠 Query Data Using Amazon Athena**  
1️⃣ Open **Amazon Athena**.  
2️⃣ Select the **Glue Catalog database** and run:  
```sql
SELECT * FROM stock_data LIMIT 10;
```

---

## **⚡ Challenges & Solutions**  
### **🔹 Inconsistent Message Processing Due to Network Latency**  
✔ Adjusted Kafka producer batch size & compression to optimize network usage.  

### **🔹 S3 Data Not Reflecting in Athena Queries**  
✔ Enabled **schema evolution in Glue** & ensured the Glue Crawler runs after new data ingestion.  

### **🔹 Consumer Lag in Kafka Processing**  
✔ Tuned Kafka consumer configurations (`auto.offset.reset = 'earliest'`).  

### **🔹 IAM Permission Issues Prevented Glue from Accessing S3**  
✔ Created a dedicated IAM role with **AmazonS3FullAccess & AWSGlueServiceRole**.  

### **🔹 Slow Query Performance in Athena**  
✔ Implemented **partitioning & compression** for optimized query speed & cost efficiency.  

---

## **🎯 Final Results**  
✅ **Real-time data pipeline from Kafka → S3 → Glue → Athena**  
✅ **Optimized for high-throughput, low-latency analytics**  
✅ **Scalable, cost-effective solution for real-time financial data analysis**  

---
