# Creating a 🔁 CI/CD Pipeline on AWS with CodePipeline

This is my project documentation for setting up a CI/CD pipeline on AWS using multiple AWS services. The following sections outline the steps I took in each phase of the project.

---

## Table of Contents
1. [Set Up a Web App in the Cloud](#set-up-a-web-app-in-the-cloud)
2. [Connect a GitHub Repo with AWS](#connect-a-github-repo-with-aws)
3. [Secure Project Dependencies with AWS CodeArtifact](#secure-project-dependencies-with-aws-codeartifact)
4. [Package an App with AWS CodeBuild](#package-an-app-with-aws-codebuild)
5. [Deploy an App with AWS CodeDeploy](#deploy-an-app-with-aws-codedeploy)
6. [Automate with AWS CloudFormation](#automate-with-aws-cloudformation)
7. [CI/CD with CodePipeline](#cicd-with-codepipeline)

---

## 🔁 Set Up a Web App in the Cloud

This section outlines how I set up an AWS EC2 instance, connected it to VSCode, and built a web application using Maven and Java.

### **Steps I followed:**

### 1. Set up an IAM user
An **IAM user** is a person or application that can securely access AWS services. Instead of using the root account for daily work, AWS recommends creating IAM users to prevent security breaches.

- Logged into my AWS root account.
- Opened the **IAM Console** and created a new IAM user named `Yourname-IAM-Admin`.
- Selected the **AdministratorAccess** policy to attach permissions.
- Downloaded the `.csv` file with the IAM user’s credentials.
- Logged out of the root account and logged back in as `Yourname-IAM-Admin`.

📌 **Screenshot Placeholder:** Add a screenshot of the IAM user creation page.

---

### 2. Launch an EC2 Instance
To host the web app, I launched an **EC2 instance** (Amazon Elastic Compute Cloud), which is like a virtual computer in the cloud.

1. Opened the **EC2 Console** and clicked on **Launch Instances**.
2. Selected **Amazon Linux 2023 AMI** as the operating system.
3. Used the default **t2.micro** instance type for cost efficiency.
4. Created a **key pair** named `nextwork-keypair` for secure SSH access.
   - AWS automatically downloaded the `.pem` file for the key pair.
5. Configured the network settings:
   - Allowed SSH traffic from **My IP** to ensure only I could connect securely.
6. Clicked **Launch Instance** and confirmed the setup.

📌 **Screenshot Placeholder:** Add a screenshot of the EC2 instance details, including the public IPv4 address.

---

### 3. Install and Set Up VSCode
**Visual Studio Code (VSCode)** is a powerful IDE (Integrated Development Environment) that allows users to write and manage code efficiently. I used it to edit the web app and connect to my EC2 instance.

1. Downloaded and installed **VSCode** from the official website.
2. Opened the terminal in VSCode and navigated to the folder containing the `.pem` file:
   ```bash
   cd ~/Desktop/DevOps
   ```
3. Updated the file permissions of the `.pem` file:
   - For **Mac/Linux**:
     ```bash
     chmod 400 nextwork-keypair.pem
     ```
   - For **Windows**:
     ```bash
     icacls "nextwork-keypair.pem" /reset
     icacls "nextwork-keypair.pem" /grant:r "%USERNAME%:R"
     icacls "nextwork-keypair.pem" /inheritance:r
     ```

📌 **Screenshot Placeholder:** Add a screenshot of the VSCode terminal showing the `.pem` file permissions being updated.

---

### 4. Connect to the EC2 Instance
Using **Secure Shell (SSH)**, I connected to the EC2 instance to work on the web app securely.

- Ran the following command in the VSCode terminal:
  ```bash
  ssh -i nextwork-keypair.pem ec2-user@<YOUR_PUBLIC_IPV4_DNS>
  ```
  - Replaced `<YOUR_PUBLIC_IPV4_DNS>` with the public DNS of my EC2 instance.

📌 **Screenshot Placeholder:** Add a screenshot of the terminal showing a successful SSH connection to the EC2 instance.

---

### 5. Install Apache Maven and Amazon Corretto 8
**Apache Maven** is a package manager for Java projects, while **Amazon Corretto 8** is the version of Java I used for this project.

1. Installed **Apache Maven**:
   ```bash
   wget https://archive.apache.org/dist/maven/maven-3/3.5.2/binaries/apache-maven-3.5.2-bin.tar.gz
   sudo tar -xzf apache-maven-3.5.2-bin.tar.gz -C /opt
   echo "export PATH=/opt/apache-maven-3.5.2/bin:$PATH" >> ~/.bashrc
   source ~/.bashrc
   ```
2. Installed **Amazon Corretto 8**:
   ```bash
   sudo dnf install -y java-1.8.0-amazon-corretto-devel
   export JAVA_HOME=/usr/lib/jvm/java-1.8.0-amazon-corretto.x86_64
   export PATH=/usr/lib/jvm/java-1.8.0-amazon-corretto.x86_64/jre/bin/:$PATH
   ```

📌 **Screenshot Placeholder:** Add screenshots of the terminal output confirming Maven and Java installations.

---

### 6. Create the Application
Using **Maven**, I generated a Java web app with the following commands:
```bash
mvn archetype:generate \
   -DgroupId=com.nextwork.app \
   -DartifactId=nextwork-web-project \
   -DarchetypeArtifactId=maven-archetype-webapp \
   -DinteractiveMode=false
```

- Maven created the following important folders:
  - `src`: Contains the source code for the web app.
  - `webapp`: Holds HTML, CSS, and JavaScript files for the web app.

📌 **Screenshot Placeholder:** Add a screenshot of the Maven-generated project structure in the VSCode file explorer.

---

### 7. Edit and Verify the Web App
I edited the `index.jsp` file, the main entry point for the Java web app, as follows:
```html
<html>
<body>
<h2>Hello Justin!</h2>
<p>This is my NextWork web application working!</p>
</body>
</html>
```

- Saved the changes using **Ctrl+S** (Windows) or **Cmd+S** (Mac).
- Verified that the dot next to the file name disappeared after saving.

📌 **Screenshot Placeholder:** Add a screenshot showing the edited `index.jsp` file in VSCode.

---

## 🔁 Connect a GitHub Repo with AWS

📌 **Placeholder for documentation steps.**

---

## 🔁 Secure Project Dependencies with AWS CodeArtifact

📌 **Placeholder for documentation steps.**

---

## 🔁 Package an App with AWS CodeBuild

📌 **Placeholder for documentation steps.**

---

## 🔁 Deploy an App with AWS CodeDeploy

📌 **Placeholder for documentation steps.**

---

## 🔁 Automate with AWS CloudFormation

📌 **Placeholder for documentation steps.**

---

## 🔁 CI/CD with CodePipeline

📌 **Placeholder for documentation steps.**

---

## Summary
In this project, I successfully:
- Set up an IAM user for secure AWS access.
- Deployed a virtual server (EC2 instance) in the cloud.
- Installed and configured Maven and Java to create a Java web app.
- Used VSCode to connect to and edit the web app on the EC2 instance.

This project laid a solid foundation for building a CI/CD pipeline with AWS services like **CodePipeline**, **CodeBuild**, and **CodeDeploy**. I look forward to completing the next parts of this series!
