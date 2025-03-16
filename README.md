# Launching a Web Server With Amazon EC2

## 📌 Project Overview
This project provides an overview of launching an **Amazon EC2 instance**. Amazon EC2 is a web service that provides **resizable compute capacity** in the cloud, enabling developers to scale their applications efficiently.

### 🎯 Objectives
By completing this lab, I successfully: </br>
✅ Launched a web server on an Amazon EC2 instance.  
✅ Modified the **security group** to allow HTTP access.    
✅ Used **User Data** to automate web server deployment.  

---

## **1️⃣ Launching an EC2 Instance**

### **Step 1: Naming the EC2 Instance**
1. In the **AWS Management Console**, go to **EC2**.
2. Click **Launch Instance**.
![image](https://github.com/user-attachments/assets/b58fe5f0-0f5c-4d9b-bb35-567e6772a33e)

4. In the **Name** field, enter `Web Server`.
![image](https://github.com/user-attachments/assets/02cd441c-1ab7-40de-9a36-1dc82028146a)

### **Step 2: Choosing an Amazon Machine Image (AMI)**
1. In the **Application and OS Images (Amazon Machine Image)** section, select `Amazon Linux 2023 AMI` (default selection).
![image](https://github.com/user-attachments/assets/dc4210d8-fdc7-42ef-8c11-da20adfd2081)

### **Step 3: Choosing an Instance Type**
1. Select **t3.micro** (2 vCPUs, 1 GiB RAM).
![image](https://github.com/user-attachments/assets/a905162a-8bb3-49a4-8d67-5066162c956c)
  
### **Step 4: Configuring Network Settings**
1. Click **Edit** in the **Network Settings** section.
2. For **VPC**, select `Lab VPC`.
![image](https://github.com/user-attachments/assets/74a9c4dc-d8e1-4ff5-93ec-a8814cd2afd1)

4. Configure the **Security Group**:
   - **Name:** `Web Server Security Group`
   - **Description:** `Security group for my web server`
   - **Inbound Rules:** Remove SSH access to improve security.
  ![image](https://github.com/user-attachments/assets/cfd52dc3-ac32-482a-b2b4-b6d4f7ee74c1)

### **Step 5: Adding Storage**
1. Keep the default **8 GiB** storage volume.
![image](https://github.com/user-attachments/assets/b0c2287e-1fe0-4ac8-9f5c-7eb87d594622)

### **Step 6: Configuring Advanced Details (User Data)**
1. Expand the **Advanced Details** section.
2. Add the following **User Data script** to automate web server setup:
   ```bash
   #!/bin/bash
   yum -y install httpd
   systemctl enable httpd
   systemctl start httpd
   echo '<html><h1>Hello From Your Web Server!</h1></html>' > /var/www/html/index.html
   ```
   ![image](https://github.com/user-attachments/assets/081b5cb2-9605-43db-a56b-272487418fb3)
   🔹 **What this script does:**  
   ✅ Installs **Apache (httpd)** web server.  
   ✅ Enables automatic startup.  
   ✅ Creates a basic **HTML page**.

### **Step 7: Launching the Instance**
1. Click **Launch Instance**.
![image](https://github.com/user-attachments/assets/aa616f14-1674-49bb-acc5-c589e5a2123a)

3. Go to **View All Instances**.
4. Wait for the instance state to become **Running and 3/3 checks passed**.
![image](https://github.com/user-attachments/assets/f4ad77b0-6ba6-439d-9722-c227e4d41867) 
![image](https://github.com/user-attachments/assets/f82683e5-8e89-4eed-990c-8c82e3e18154)  

---

## **2️⃣ Updating Security Group & Accessing the Web Server**

### **Step 1: Copy Public IPv4 Address**
1. In the **EC2 Console**, go to **Instances**.
2. Select your `Web Server` instance.
3. Copy the **Public IPv4 address**.
![image](https://github.com/user-attachments/assets/82b08b9a-9058-4d9e-b7cd-e781d39712a5)

5. Open a new browser tab and enter the copied IP.
![image](https://github.com/user-attachments/assets/b0a7798f-6d90-4573-9c92-2d486895fa69)
🔴 **Expected Result:** The page won’t load because HTTP access is blocked by the security group.

### **Step 2: Update Security Group to Allow HTTP Access**
1. In the **AWS EC2 Console**, go to **Security Groups**.
![image](https://github.com/user-attachments/assets/07a57d82-432c-4609-9f41-31f9c00f4200)

3. Select `Web Server Security Group`.
![image](https://github.com/user-attachments/assets/ee127eda-66c7-4b0e-a8b8-194886f5da25)

5. Click **Inbound Rules → Edit Inbound Rules**.
![image](https://github.com/user-attachments/assets/4654b44f-983c-4c25-baa7-8e0fdf67f82f)

7. Click **Add Rule** and configure:
   - **Type:** HTTP  
   - **Source:** Anywhere - IPv4  (Just for the purpose of this demo, I'm setting it up to be accessible from any IP direction, but in a real environment following best security practices should allow only known IPs)
8. Click **Save Rules**.
![image](https://github.com/user-attachments/assets/77913840-ffa9-497b-a611-4ce95aa566c0)

### **Step 3: Test Web Server Access**
1. Return to the browser tab with the public IP.
2. **Refresh the page**.
3. ✅ **Expected Output:** `Hello From Your Web Server!`  
![image](https://github.com/user-attachments/assets/06596a58-284b-489c-a623-a0db056bc4a7)
---

## **🚀 Conclusion**
This project successfully demonstrated how to: </br>
✅ Launch an **Amazon EC2 instance**.  
✅ Deploy an **Apache web server** using **User Data**.  
✅ Secure the instance by configuring a **Security Group**.  
✅ Modify firewall rules to enable **HTTP access**.  

This setup is a **foundational skill** for deploying web applications in AWS.









