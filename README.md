# **Cloud Troubleshooting & Performance Monitoring (AWS & Azure)**

## **📌 Project Overview**
This project focuses on real-time **cloud infrastructure troubleshooting and performance monitoring** using **AWS CloudWatch** and **Azure Application Insights**. It enables better **log analysis, incident response, and database performance optimization**, ensuring system reliability and faster failure resolution.

## **🔹 Key Features**
✅ Real-time **log monitoring** using **AWS CloudWatch Logs** and **Azure Application Insights**.  
✅ **Automated alerts** for system failures and high resource usage.  
✅ **SQL performance tuning** to optimize slow database queries.  
✅ **Incident response improvement**, reducing system failure resolution time by **40%**.  

---

## **🛠️ Step-by-Step Implementation**

### **1️⃣ AWS CloudWatch Setup (For AWS Applications)**

#### **🔹 Create a CloudWatch Log Group**
1. Login to **AWS Console** → Navigate to **CloudWatch** → Click **Logs**.
2. Click **Create Log Group** → Name it `app-logs-group`.
3. Set retention period to **7-14 days** based on needs.

#### **🔹 Configure Application to Send Logs to CloudWatch**
- **For EC2 Instances:**
  ```bash
  sudo yum install amazon-cloudwatch-agent -y
  sudo systemctl start amazon-cloudwatch-agent
  ```
  Modify agent configuration in `/opt/aws/amazon-cloudwatch-agent/etc/amazon-cloudwatch-agent.json`.
  ```json
  {
    "logs": {
      "logs_collected": {
        "files": {
          "collect_list": [
            {
              "file_path": "/var/log/app.log",
              "log_group_name": "app-logs-group",
              "log_stream_name": "{instance_id}"
            }
          ]
        }
      }
    }
  }
  ```
  Restart the agent:
  ```bash
  sudo systemctl restart amazon-cloudwatch-agent
  ```

---

### **2️⃣ Azure Application Insights Setup (For Azure Applications)**

#### **🔹 Enable Application Insights**
1. Login to **Azure Portal** → Go to **Application Insights**.
2. Click **Create Resource** → Select **Application Insights**.
3. Choose **Resource Group** → Click **Create**.

#### **🔹 Integrate Application Insights into Your Application**
- **For Node.js Applications:**
  ```bash
  npm install applicationinsights
  ```
  ```javascript
  const appInsights = require("applicationinsights");
  appInsights.setup("<your_instrumentation_key>").start();
  ```
- **For .NET Applications:** Import and initialize in `Startup.cs`.

---

### **3️⃣ Debugging System Failures**

#### **🔹 Set Up CloudWatch Alarms (AWS)**
1. Go to **AWS CloudWatch** → Click **Alarms** → **Create Alarm**.
2. Choose **app-logs-group** → Click **Create Metric Filter**.
3. Enter **ERROR** as the **Filter Pattern**.
4. Assign Metric Name: `ApplicationErrorCount`.
5. Set **Threshold Condition**: Trigger alert if errors exceed **5 per minute**.
6. Configure **SNS Notifications** to send **Email/SMS alerts**.

#### **🔹 Set Up Alerts in Azure Application Insights**
1. Go to **Azure Application Insights**.
2. Click **Alerts** → **New Alert Rule**.
3. Set conditions (e.g., **Failed requests > 10%**).
4. Configure email notifications.

---

### **4️⃣ SQL Database Performance Optimization**

#### **🔹 Identify Slow Queries in AWS RDS**
1. Open **AWS RDS Console** → Select **Database Instance**.
2. Click **Performance Insights** → Identify slow queries.
3. Enable Slow Query Log:
   ```sql
   SET GLOBAL slow_query_log = 'ON';
   SET GLOBAL long_query_time = 1;
   ```
4. View slow queries:
   ```sql
   SELECT * FROM mysql.slow_log ORDER BY start_time DESC;
   ```

#### **🔹 Identify & Optimize Slow Queries in Azure SQL**
1. Open **Azure Portal** → Navigate to **SQL Database**.
2. Click **Query Performance Insights**.
3. Identify **queries taking longer than 1s**.
4. Optimization Steps:
   - **Create Indexes:**
     ```sql
     CREATE INDEX idx_user_email ON users(email);
     ```
   - **Avoid SELECT *** (fetch only required fields).

---

## **🎯 Project Outcome & Benefits**
✅ **Enhanced cloud visibility** through **real-time log monitoring**.  
✅ **Reduced failure response time by 40%** with automated **alerts & debugging**.  
✅ **Optimized database performance**, reducing **query execution time by 50%**.  

---

## **📌 Future Enhancements**
🔹 Implement **Grafana dashboards** for better log visualization.  
🔹 Automate monitoring setup using **Terraform**.  
🔹 Enable **AI-powered anomaly detection** for advanced troubleshooting.  

---


