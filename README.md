# CI/CD Pipeline Using AWS Cloud Services

This repository contains the setup and configuration for a **CI/CD pipeline** using **AWS Cloud Services** and essential DevOps tools. The pipeline automates the following stages: fetching code, building, testing, analyzing code, and uploading artifacts.

---

## **Pipeline Overview**

### **Stages of the Pipeline**
1. **Fetch Code**: 
   - The source code is pulled from a Git repository.
   - Version control ensures that the latest code changes are fetched for the pipeline.

2. **Build**: 
   - Code is compiled using **Maven** to generate build artifacts (e.g., `.jar` or `.war` files).
   - Dependencies are resolved, and the project is packaged.

3. **Unit Testing**:
   - Unit tests are executed using **Maven**.
   - Test results are generated to ensure code quality and identify any regressions.

4. **Code Analysis**:
   - The code is analyzed using **SonarQube Server** to identify issues such as bugs, vulnerabilities, and code smells.
   - SonarQube provides a detailed report of the code’s quality.

5. **Upload Artifact**:
   - The generated artifact is uploaded to **Nexus OSS (Open Source Software Repository)**.
   - Nexus serves as a centralized repository to store and manage build artifacts for further deployment.

---

## **Tools and Technologies**

### **Core Tools**
- **AWS EC2**:
  - EC2 instances host the necessary tools (e.g., SonarQube, Nexus, Jenkins) and execute the pipeline stages.
- **Git**: 
  - Source control system for managing the codebase.
- **Maven**:
  - Build automation tool for Java projects.
- **SonarQube**:
  - Platform for static code analysis and quality checks.
- **Nexus OSS**:
  - Repository manager for storing build artifacts.

### **Other Technologies**
- **Jenkins**:
  - CI/CD automation server to orchestrate the pipeline.

---

## **Setup Instructions**

### **Prerequisites**
1. **AWS Setup**:
   - Launch EC2 instances for Jenkins, SonarQube, and Nexus OSS.
   - Configure security groups to allow communication between the instances (e.g., open ports for SSH, Nexus (8081), SonarQube (9000), and Jenkins (8080)).
2. **Installations**:
   - Install Jenkins, Maven, SonarQube, and Nexus OSS on their respective EC2 instances.

### **Pipeline Configuration**
1. **Step 1: Fetch Code**  
   - Configure Jenkins to pull the code from a Git repository (e.g., GitHub or Bitbucket).

2. **Step 2: Build**  
   - Add a build stage in Jenkins to run the following Maven command:
     ```bash
     mvn clean package
     ```

3. **Step 3: Unit Test**  
   - Execute Maven unit tests in the pipeline:
     ```bash
     mvn test
     ```

4. **Step 4: Code Analysis**  
   - Integrate SonarQube with Jenkins using the **SonarQube Scanner Plugin**.
   - Add a SonarQube analysis stage in Jenkins:
     ```bash
     sonar-scanner -Dsonar.projectKey=your_project_key \
                   -Dsonar.sources=src/ \
                   -Dsonar.host.url=http://<SonarQube-Private-IP>:9000 \
                   -Dsonar.login=<SonarQube-Auth-Token>
     ```

5. **Step 5: Upload Artifact**  
   - Add a Nexus artifact upload stage using **curl** or **Jenkins Nexus Artifact Uploader Plugin**:
     ```bash
     curl -v -u admin:admin123 --upload-file target/your-artifact.jar \
          http://<Nexus-Private-IP>:8081/repository/your-repo/
     ```

---

## **Pipeline Workflow**

### **Pipeline Diagram**
```text
Git Repository 
    |
    v
Fetch Code (Git)
    |
    v
Build (Maven)
    |
    v
Unit Test (Maven)
    |
    v
Code Analysis (SonarQube)
    |
    v
Upload Artifact (Nexus OSS)
```

### **Triggering the Pipeline**
- The pipeline can be triggered automatically on every code push using **webhooks** or manually through Jenkins.

---

## **Expected Outcomes**
- **Build Artifacts**:
  - Compiled code will be packaged and stored in Nexus OSS.
- **Quality Reports**:
  - SonarQube will provide insights into code quality and identify areas for improvement.
- **Continuous Integration**:
  - Code is automatically built, tested, and analyzed after every commit.

---

## **Future Enhancements**
1. **Add Deployment Stage**:
   - Automate the deployment of the artifact to a staging or production environment.
2. **Dockerize the Setup**:
   - Use Docker containers for Jenkins, SonarQube, and Nexus to simplify management and scalability.
3. **AWS CodePipeline**:
   - Migrate to AWS CodePipeline for native integration with other AWS services.

---

## **Contact**
For any questions or issues, feel free to reach out:

- **Name**: Damilare Adeyoyin
- **Role**: DevOps Engineer
- **Email**: dammyyoyin@gmail.com
