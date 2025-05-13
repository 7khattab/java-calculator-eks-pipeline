
# **Calculator REST API with CI/CD on AWS EKS**

This repository contains the code and configurations for a **Calculator REST API** built with **Java** and **Spring Boot**. The application provides basic arithmetic operations via a REST API, such as addition, subtraction, multiplication, and division. This project also includes a fully automated CI/CD pipeline using **GitHub Actions** and **AWS EKS** for deployment.

---

## **Project Overview**

### **What does the app do?**

The **Calculator REST API** allows users to perform basic arithmetic operations over HTTP requests. It provides the following operations:

* **Addition** (`/api/calculator/add?a={number}&b={number}`)
* **Subtraction** (`/api/calculator/subtract?a={number}&b={number}`)
* **Multiplication** (`/api/calculator/multiply?a={number}&b={number}`)
* **Division** (`/api/calculator/divide?a={number}&b={number}`)

### **Components of the Application**

1. **Calculator.java**: Contains the logic for performing arithmetic operations.
2. **CalculatorController.java**: The REST controller that handles incoming requests and calls methods from `Calculator.java` to perform the operations.
3. **App.java**: The entry point for the Spring Boot application.
4. **application.properties**: Configuration file for setting up server port and other configurations.

---

## **Technologies Used**

* **Java 17**: The programming language used to develop the API.
* **Spring Boot 2.7.x**: The framework used for building the REST API.
* **AWS EKS**: Amazon Elastic Kubernetes Service used to manage and deploy the application on AWS.
* **Docker**: Used to containerize the application for deployment.
* **GitHub Actions**: CI/CD pipeline for automating the build, test, and deployment processes.
* **AWS IAM**: For managing roles and permissions.

---

## **Steps Taken to Deploy the App**

### **1. Set Up AWS EKS Cluster**

To deploy the application to **AWS EKS**:

* Created an **EKS Cluster** on AWS.
* Configured the **Node Group** to define the EC2 instances that will run the Kubernetes nodes.
* Set IAM roles and permissions for the Kubernetes cluster and node groups.

### **2. Dockerization**

The application was containerized using **Docker**:

* Created a `Dockerfile` that builds a Docker image for the application.
* The image was pushed to **Docker Hub** to make it available for deployment.

### **3. CI/CD Pipeline with GitHub Actions**

The **CI/CD pipeline** automates the entire workflow from code push to deployment:

* The pipeline builds the application and runs unit tests using `mvn test`and Run Integration Tests and Package.
* It then builds a Docker image and pushes it to Docker Hub using **Docker Buildx**.
* Finally, the application is deployed to the **AWS EKS cluster** using `kubectl apply` to manage Kubernetes deployment and service configurations.

#### **CI/CD Workflow Breakdown**

1. **Build and Test**:

   * The code is built using Maven (`mvn clean install`), unit tests are executed (`mvn test`) and Run Integration Tests and Package ('mvn clean package')

2. **Docker Build & Push**:

   * The application is packaged into a Docker image using the `Dockerfile`.
   * The image is pushed to **Docker Hub**.

3. **Deploy to Kubernetes**:

   * The CI/CD pipeline configures AWS credentials and uses `kubectl` to update the Kubernetes configuration (`aws eks update-kubeconfig`).
   * The application is deployed to the **EKS cluster** using the Kubernetes manifests (`deployment.yaml` and `service.yaml`).

---

## **Kubernetes Configuration**

* **Deployment**: Specifies how to deploy the application using **3 replicas** for high availability.
* **Service**: Exposes the application on port **80** and maps it to container port **8080**.

### **AWS EKS**:

* **EKS Cluster**: Manages Kubernetes resources in the cloud.
* **Node Groups**: Specifies the EC2 instances that will host the Kubernetes nodes.
* **IAM Roles**: Used to securely grant the application permissions for accessing AWS services.

---

## **How to Run the Project Locally**

To run this project locally on your machine:

1. Clone the repository:

   ```bash
   git clone https://github.com/your-username/calculator-api.git
   cd calculator-api
   ```

2. Build and run the application:

   ```bash
   mvn spring-boot:run
   ```

3. The application will be accessible at `http://localhost:8080`.



## **CI/CD Process**

Once the **CI/CD pipeline** is triggered by a `push` to the `main` branch:

1. **Code is checked out** from GitHub.
2. **Unit tests** are executed.
3. **integration tests**
4. **Docker image** is built and pushed to **Docker Hub**.
5. **AWS credentials** are configured, and the application is deployed to **EKS** using Kubernetes manifests.

---

## **Conclusion**

This project demonstrates a fully automated **CI/CD pipeline** for deploying a **Spring Boot Calculator REST API** to **AWS EKS**. It uses **Docker**, **GitHub Actions**, and **Kubernetes** to manage the deployment lifecycle and ensure that the app is always running and up-to-date.


