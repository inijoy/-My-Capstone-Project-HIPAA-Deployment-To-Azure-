# My Capstone Project. HIPAA Deployment To Azure

## HIPAA Deployment to Azure

# **Problem Statement**

The company currently faces several **critical challenges** that hinder its ability to maintain a reliable, secure, and scalable cloud infrastructure. These challenges include:

### **1.1 Frequent Downtime & Poor Reliability**

- The company’s existing infrastructure is **monolithic**, creating a **single point of failure**, leading to frequent **service interruptions** and **downtime** during high traffic or system updates.
- **Manual scaling processes** are inefficient and fail to meet the demand during peak times, further contributing to **performance issues** and **unpredictable uptime**.

### **1.2 Inefficient Continuous Integration & Deployment (CI/CD)**

- The current deployment process is **manual and error-prone**, making it time-consuming and inconsistent. This results in **delayed feature releases**, inconsistent environments, and slower response to critical bug fixes and security patches.
- The company lacks a **fully automated CI/CD pipeline**, which would streamline development and operations, ensuring that new features and updates are deployed seamlessly and without human intervention.

### **1.3 Compliance & Security Challenges (HIPAA)**

- The company handles **sensitive healthcare data**, which requires adherence to **HIPAA regulations** for **data security** and **privacy**. However, their current infrastructure does not meet the necessary **security standards**, including **encryption**, **access control**, and **audit trails**, putting patient data at risk.
- Ensuring **compliance with HIPAA** is a major concern, as the lack of robust security measures could lead to costly penalties, legal repercussions, and damage to the company’s reputation.

### **1.4 Lack of Visibility & Monitoring**

- The company has limited **real-time visibility** into the performance and health of their applications and infrastructure.
- Without proper **monitoring tools**, the team struggles to identify and address **performance bottlenecks**, **security threats**, or other operational issues before they escalate.

### **1.5 Inadequate Incident Management & Alerting**

- The existing incident management system is reactive rather than proactive, leading to slow responses to **critical system failures**, security breaches, or performance issues.
- The company lacks an integrated alerting system for immediate notification of critical events. Without **automated alerts** or **Slack integration**, the DevOps and operations teams face delays in identifying and addressing issues, affecting system uptime and user experience.

# **Project Objective**

To resolve these challenges, I designed and deployed a **scalable, HIPAA-compliant microservices application** on **Kubernetes** in **Azure**, with integrated solutions to address the core issues, including:

- **Ensuring high availability and reliability** through Kubernetes for auto-scaling and fault tolerance.
- **Automating deployments and updates** via a CI/CD pipeline using **GitHub Actions**.
- **I**mplement **RBAC**, **TLS encryption**, and **secure data storage to meet HIPAA compliance**.
- **Implementing comprehensive monitoring** with **Datadog** for real-time performance tracking and **Slack notifications** for proactive incident alerting.

---

### 

# 1. Deployment to Kubernetes to Azure

### **1. Architecture of the Kubernetes Infrastructure**

**Overview:** The deployment architecture for the Kubernetes infrastructure was designed to meet HIPAA compliance standards. 

I designed our Kubernetes infrastructure deployment with HIPAA compliance in mind.

 **Details:**

- A highly available AKS cluster, so you can count on it being always on.
- Network policies and security configurations that meet HIPAA standards, give you peace of mind.
- I use Azure resources like Virtual Networks (VNets) and Network Security Groups (NSGs) to keep everything running smoothly and securely.
- The architecture includes a highly available AKS cluster with node pools for specific workloads.
- Network policies and security configurations were implemented for compliance.

**Image Placeholder: The Architecture**

![Screenshot 2025-02-19 173725.png AZURE ARCHITECTURE.png](My%20Capstone%20Project%20HIPAA%20Deployment%20To%20Azure%2019f5c4233bb6806987cbd5f490868722/Screenshot_2025-02-19_173725.png_AZURE_ARCHITECTURE.png)

### Overview

This project documents the end-to-end deployment of a HIPAA-compliant infrastructure on Azure using Terraform, GitHub Actions, Kubernetes, and OpenLens. Below is a step-by-step breakdown of the setup, including infrastructure provisioning, CI/CD implementation, and application deployment.

## Step-by-Step Process

### **1. Infrastructure as Code with Terraform**

- Created a workspace on Terraform Cloud (`hijo-terraform`) and initialized the following infrastructure files:
    - `backend.tf` (remote state configuration)
    - `provider.tf` (Azure provider settings)
- `resource-group.tf` (resource group creation)
- `network.tf` (virtual network and subnet)
- `aks.tf` (Azure Kubernetes Service cluster setup)
- `nginx.tf` (Nginx Ingress Controller)
- `cert-manager.tf` (SSL certificate automation)
- `cicd.yml` (GitHub Actions CI/CD pipeline)

*Screenshot Placeholder: Terraform File Structure in VS Code)*

![Screenshot 2025-02-19 182702.png](My%20Capstone%20Project%20HIPAA%20Deployment%20To%20Azure%2019f5c4233bb6806987cbd5f490868722/Screenshot_2025-02-19_182702.png)

### **2. GitHub Repository and Secrets Setup**

- Created a private repository: `KubernetesAZURE`.
- Configured GitHub Secrets for authentication and deployment:
    - `AZURE_CLIENT_ID`, `AZURE_CLIENT_SECRET`, `AZURE_SUBSCRIPTION_ID`, `AZURE_TENANT_ID`
    - `TF_API_TOKEN`, `REGISTRY_NAME`, `AKS_CLUSTER`, `SLACK_WEBHOOK_URL`

*(Screenshot Placeholder: GitHub Secrets Configuration)*

![Screenshot 2025-02-19 184518.png GitHub Repository and Secrets Setup.png](My%20Capstone%20Project%20HIPAA%20Deployment%20To%20Azure%2019f5c4233bb6806987cbd5f490868722/Screenshot_2025-02-19_184518.png_GitHub_Repository_and_Secrets_Setup.png)

### **3. Terraform Deployment and AKS Configuration**

- Ran Terraform commands to provision Azure infrastructure:
    
    ```
    terraform init
    terraform plan
    terraform apply -auto-approve
    ```
    
- Used `az cli` to authenticate and connect Kubernetes cluster to OpenLens.

*(Screenshot Placeholder: AKS Cluster in Azure Portal )*

![Screenshot 2025-02-13 034732.PNG AKS CLUSTER IN AZURE PORTAL.PNG 1.PNG](My%20Capstone%20Project%20HIPAA%20Deployment%20To%20Azure%2019f5c4233bb6806987cbd5f490868722/Screenshot_2025-02-13_034732.PNG_AKS_CLUSTER_IN_AZURE_PORTAL.PNG_1.png)

### **4. Database Configuration**

- Created `Azure Database for MySQL` (Flexible Server).
- Set up firewall rules for secure access.
- Connected via MySQL Workbench.

*(Screenshot Placeholder: MySQL Workbench Connected to Azure Database)*

![Screenshot 2025-02-13 035204.PNG DATABASE CONFIGURATION.PNG](My%20Capstone%20Project%20HIPAA%20Deployment%20To%20Azure%2019f5c4233bb6806987cbd5f490868722/Screenshot_2025-02-13_035204.PNG_DATABASE_CONFIGURATION.png)

### **5. DNS and SSL Setup**

- Configured DNS on Namecheap with custom domains:
    - `hospital.api` → Load Balancer IP
    - `hospital.hijo-cloud.online` → Web application
- Verified SSL certificate using `cert-manager`.

*(Screenshot Placeholder: Namecheap DNS Settings & SSL Certificate Details)*

![Screenshot 2025-02-13 035624.PNG NAMECHEAP DNS.PNG](My%20Capstone%20Project%20HIPAA%20Deployment%20To%20Azure%2019f5c4233bb6806987cbd5f490868722/Screenshot_2025-02-13_035624.PNG_NAMECHEAP_DNS.png)

![Screenshot 2025-02-13 031637.png CERTIFICATE DETAILS.png](My%20Capstone%20Project%20HIPAA%20Deployment%20To%20Azure%2019f5c4233bb6806987cbd5f490868722/Screenshot_2025-02-13_031637.png_CERTIFICATE_DETAILS.png)

### **6. Backend Deployment**

- Created a Docker Hub repository (`adminhijo/hospital-app-backend`).
- Implemented GitHub Actions for automated build and deployment.
- Deployed backend services using Kubernetes manifests.

*(Screenshot Placeholder: OpenLens Showing Running Backend Pods)*

![Screenshot 2025-02-13 030509.png RUNNING PODS.png](My%20Capstone%20Project%20HIPAA%20Deployment%20To%20Azure%2019f5c4233bb6806987cbd5f490868722/Screenshot_2025-02-13_030509.png_RUNNING_PODS.png)

![Screenshot 2025-02-13 035330.png DOCKER REPO.png](My%20Capstone%20Project%20HIPAA%20Deployment%20To%20Azure%2019f5c4233bb6806987cbd5f490868722/Screenshot_2025-02-13_035330.png_DOCKER_REPO.png)

![Screenshot 2025-02-19 210819.png GITACTION BACKEND AZURE.png](My%20Capstone%20Project%20HIPAA%20Deployment%20To%20Azure%2019f5c4233bb6806987cbd5f490868722/Screenshot_2025-02-19_210819.png_GITACTION_BACKEND_AZURE.png)

### **7. Frontend Deployment**

- Set up a `React` frontend repository on GitHub (`main_hospital_frontend_app`).
- Configured Kubernetes manifests (`configmap.yaml`, `ingress.yaml`, `service.yaml`).
- Deployed frontend application to Kubernetes.
    
    ![Screenshot 2025-02-13 030509.png RUNNING PODS.png](My%20Capstone%20Project%20HIPAA%20Deployment%20To%20Azure%2019f5c4233bb6806987cbd5f490868722/Screenshot_2025-02-13_030509.png_RUNNING_PODS%201.png)
    

*(Screenshot Placeholder: OpenLens Showing Running Frontend Pods)*

![Screenshot 2025-02-13 035330.png DOCKER REPO.png](My%20Capstone%20Project%20HIPAA%20Deployment%20To%20Azure%2019f5c4233bb6806987cbd5f490868722/Screenshot_2025-02-13_035330.png_DOCKER_REPO%201.png)

![Screenshot 2025-02-19 214858.png FRONTENDGIT ACTION DEPLOYMENT.png](My%20Capstone%20Project%20HIPAA%20Deployment%20To%20Azure%2019f5c4233bb6806987cbd5f490868722/Screenshot_2025-02-19_214858.png_FRONTENDGIT_ACTION_DEPLOYMENT.png)

1. **Slack Notification of Repository Push**

**Overview:** A Slack notification was triggered to the alert channel upon the repository push.

**Details:**

- The configured webhook successfully sent a notification to Slack.
- The alert contained details about the commit and user.

**Image Placeholder:**

![Screenshot 2025-02-19 221003.png SLACK ALERT FOR AZURE HIPPA DEPLOYMENT.png](My%20Capstone%20Project%20HIPAA%20Deployment%20To%20Azure%2019f5c4233bb6806987cbd5f490868722/Screenshot_2025-02-19_221003.png_SLACK_ALERT_FOR_AZURE_HIPPA_DEPLOYMENT.png)

### **9. Successful Deployment of a secured Hospital Frontend -(Dental Management App)**

- Accessed deployed application via `hospital.hijo-cloud.online`.
- Validated functionality, SSL security, and database integration.
- Documented deployment process in a walkthrough video.

*(Video Placeholder: Website Deployment )*

![Screenshot 2025-02-19 220338.png App Screenshot.png](My%20Capstone%20Project%20HIPAA%20Deployment%20To%20Azure%2019f5c4233bb6806987cbd5f490868722/Screenshot_2025-02-19_220338.png_App_Screenshot.png)

# Additional Screenshots review:

![Screenshot 2025-02-12 234035.png](My%20Capstone%20Project%20HIPAA%20Deployment%20To%20Azure%2019f5c4233bb6806987cbd5f490868722/Screenshot_2025-02-12_234035.png)

![Screenshot 2025-02-13 001141.png](My%20Capstone%20Project%20HIPAA%20Deployment%20To%20Azure%2019f5c4233bb6806987cbd5f490868722/Screenshot_2025-02-13_001141.png)

![Screenshot 2025-02-13 001243.png](My%20Capstone%20Project%20HIPAA%20Deployment%20To%20Azure%2019f5c4233bb6806987cbd5f490868722/Screenshot_2025-02-13_001243.png)

![Screenshot 2025-02-13 005718.png](My%20Capstone%20Project%20HIPAA%20Deployment%20To%20Azure%2019f5c4233bb6806987cbd5f490868722/Screenshot_2025-02-13_005718.png)

![Screenshot 2025-02-13 011726.png](My%20Capstone%20Project%20HIPAA%20Deployment%20To%20Azure%2019f5c4233bb6806987cbd5f490868722/Screenshot_2025-02-13_011726.png)

![Screenshot 2025-02-13 030509.png](My%20Capstone%20Project%20HIPAA%20Deployment%20To%20Azure%2019f5c4233bb6806987cbd5f490868722/Screenshot_2025-02-13_030509.png)

![Screenshot 2025-02-13 030627.png](My%20Capstone%20Project%20HIPAA%20Deployment%20To%20Azure%2019f5c4233bb6806987cbd5f490868722/Screenshot_2025-02-13_030627.png)

![Screenshot 2025-02-13 031121.png](My%20Capstone%20Project%20HIPAA%20Deployment%20To%20Azure%2019f5c4233bb6806987cbd5f490868722/Screenshot_2025-02-13_031121.png)

![Screenshot 2025-02-13 031140.png](My%20Capstone%20Project%20HIPAA%20Deployment%20To%20Azure%2019f5c4233bb6806987cbd5f490868722/Screenshot_2025-02-13_031140.png)

![Screenshot 2025-02-13 031309.png](My%20Capstone%20Project%20HIPAA%20Deployment%20To%20Azure%2019f5c4233bb6806987cbd5f490868722/Screenshot_2025-02-13_031309.png)

![Screenshot 2025-02-13 031405.png](My%20Capstone%20Project%20HIPAA%20Deployment%20To%20Azure%2019f5c4233bb6806987cbd5f490868722/Screenshot_2025-02-13_031405.png)

![Screenshot 2025-02-13 031440.png](My%20Capstone%20Project%20HIPAA%20Deployment%20To%20Azure%2019f5c4233bb6806987cbd5f490868722/Screenshot_2025-02-13_031440.png)

![Screenshot 2025-02-13 031637.png](My%20Capstone%20Project%20HIPAA%20Deployment%20To%20Azure%2019f5c4233bb6806987cbd5f490868722/Screenshot_2025-02-13_031637.png)

![Screenshot 2025-02-13 034703.png](My%20Capstone%20Project%20HIPAA%20Deployment%20To%20Azure%2019f5c4233bb6806987cbd5f490868722/Screenshot_2025-02-13_034703.png)

![Screenshot 2025-02-13 034732.png](My%20Capstone%20Project%20HIPAA%20Deployment%20To%20Azure%2019f5c4233bb6806987cbd5f490868722/Screenshot_2025-02-13_034732.png)

![Screenshot 2025-02-13 034820.png](My%20Capstone%20Project%20HIPAA%20Deployment%20To%20Azure%2019f5c4233bb6806987cbd5f490868722/Screenshot_2025-02-13_034820.png)

![Screenshot 2025-02-13 035204.png](My%20Capstone%20Project%20HIPAA%20Deployment%20To%20Azure%2019f5c4233bb6806987cbd5f490868722/Screenshot_2025-02-13_035204.png)

![Screenshot 2025-02-13 035330.png](My%20Capstone%20Project%20HIPAA%20Deployment%20To%20Azure%2019f5c4233bb6806987cbd5f490868722/Screenshot_2025-02-13_035330.png)

![Screenshot 2025-02-13 035440.png](My%20Capstone%20Project%20HIPAA%20Deployment%20To%20Azure%2019f5c4233bb6806987cbd5f490868722/Screenshot_2025-02-13_035440.png)

![Screenshot 2025-02-13 035515.png](My%20Capstone%20Project%20HIPAA%20Deployment%20To%20Azure%2019f5c4233bb6806987cbd5f490868722/Screenshot_2025-02-13_035515.png)

![Screenshot 2025-02-13 035624.png](My%20Capstone%20Project%20HIPAA%20Deployment%20To%20Azure%2019f5c4233bb6806987cbd5f490868722/Screenshot_2025-02-13_035624.png)

![Screenshot 2025-02-12 221455.png](My%20Capstone%20Project%20HIPAA%20Deployment%20To%20Azure%2019f5c4233bb6806987cbd5f490868722/Screenshot_2025-02-12_221455.png)

### **The video compilation of the deployments process**

[https://www.canva.com/design/DAGfxtnAG3E/1VMne5Gy_bW8neHkWS2nvQ/edit?utm_content=DAGfxtnAG3E&utm_campaign=designshare&utm_medium=link2&utm_source=sharebutton](https://www.canva.com/design/DAGfxtnAG3E/1VMne5Gy_bW8neHkWS2nvQ/edit?utm_content=DAGfxtnAG3E&utm_campaign=designshare&utm_medium=link2&utm_source=sharebutton)

Thank you.