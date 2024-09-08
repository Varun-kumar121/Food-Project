### Automated Deployment of a Web Application Using Jenkins, GitHub, and AWS CodeDeploy

---

## **Project Overview**

This project automates the deployment process of a web application using a CI/CD pipeline with Jenkins, GitHub, and AWS services (S3, CodeDeploy, EC2). The setup ensures that any changes pushed to the GitHub repository are automatically deployed to the production environment, reducing manual intervention and improving the efficiency of the deployment process.

---

## **Technologies and Tools Used**

- **Operating System:** Ubuntu Server
- **CI/CD Tool:** Jenkins
- **Version Control:** GitHub
- **Cloud Provider:** AWS (S3, CodeDeploy, EC2)
- **Scripting:** Shell scripting (Bash)
- **Web Technologies:** HTML (for the web application)

---

## **Project Structure**

- **Jenkinsfile:** Contains the pipeline script for automating the build, package, and deployment processes.
- **appspec.yml:** Configuration file for AWS CodeDeploy, specifying the deployment instructions.
- **source_code/:** Directory containing the web application files (e.g., HTML, CSS, JavaScript).

---

## **Setup Instructions**

### **1. Prerequisites**

- Ubuntu Server with Jenkins installed and running.
- AWS account with S3, CodeDeploy, and EC2 set up.
- GitHub repository with the application source code.

### **2. Installation and Configuration**

1. **Clone the Repository:**
   ```bash
   git clone https://github.com/Varun-kumar121/Food-Project.git
   cd Food-Project
   ```

2. **Set Up Jenkins:**
   - Install necessary Jenkins plugins:
     - GitHub Integration Plugin
     - AWS CodeDeploy Plugin
     - Pipeline Plugin

   - Configure Jenkins with GitHub and AWS credentials.

3. **Configure AWS Services:**
   - Create an S3 bucket named `food-project-deployment-bucket`.
   - Set up AWS CodeDeploy application (`MyWeb`) and deployment group (`FoodProjectDeploymentGroup`).
   - Ensure EC2 instances are correctly configured with the CodeDeploy agent and appropriate IAM roles.

4. **Configure GitHub Webhook:**
   - Navigate to `Settings` > `Webhooks` in your GitHub repository.
   - Add a new webhook with the Payload URL pointing to your Jenkins server (e.g., `http://<your-jenkins-server>:8080/github-webhook/`).
   - Select `Just the push event` as the trigger.

5. **Set Up Jenkins Pipeline:**
   - Create a Jenkins job and add the pipeline defined in the `Jenkinsfile`.

6. **Run the Pipeline:**
   - Push any changes to the `master` branch of the GitHub repository.
   - Jenkins will automatically trigger the pipeline and deploy the application to the EC2 instances.

---

## **Pipeline Overview**

The Jenkins pipeline is divided into the following stages:

1. **Clone Repository:** Fetches the latest code from the GitHub repository.
2. **Build:** Executes the build process (if applicable).
3. **Package:** Packages the application into a ZIP file for deployment.
4. **Upload to S3:** Uploads the ZIP file to the specified S3 bucket.
5. **Deploy to EC2:** Triggers AWS CodeDeploy to deploy the application to the EC2 instances.

---

## **Troubleshooting**

- **Webhook Not Triggering:** Ensure that the Jenkins server is publicly accessible and the Payload URL is correct.
- **Deployment Failures:** Verify that the `appspec.yml` file is correctly configured and present in the repository.
- **CodeDeploy Issues:** Ensure the CodeDeploy agent is running on the EC2 instances and the instances have the correct IAM roles attached.

---

## **Contributing**

Contributions are welcome! Please fork this repository and submit a pull request if you wish to contribute to the project.

---

This README file provides a comprehensive overview of the project, including setup instructions, pipeline details, and troubleshooting tips.
