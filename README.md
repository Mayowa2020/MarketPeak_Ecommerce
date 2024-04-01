# Capstone Project – E-Commerce Platform Deployment with Git, Linux, and AWS

## Scenario

You have been assigned to develop an e-commerce website for a new online marketplace named "MarketPeak." This platform will feature product listings, a shopping cart, and user authentication. Your objective is to utilize Git for version control, develop the platform in a Linux environment, and deploy it on an AWS EC2 instance.

## Tasks

### 1. Implement Version Control with Git

#### 1.1. Initialize Git Repository\*\*

\*\*
Begin by creating a project directory named "MarketPeak_Ecommerce" and initializing a Git repository inside it.

```bash
mkdir MarketPeak_Ecommerce
cd MarketPeak_Ecommerce
git init
```

#### 1.2. Obtain and Prepare the E-Commerce Website Template

Download a suitable e-commerce website template from Tooplate or any other free template resource. Extract the template into your project directory and customize it if necessary.

#### 1.3. Stage and Commit the Template to Git

Add your website files to the Git repository, set your Git global configuration, and commit your changes.

```bash
git add .
git config --global user.name "YourUsername"
git config --global user.email "youremail@example.com”
git commit -m “Initial commit with basic e-commerce site structure”
```

#### 1.4. Push the code to your GitHub repository

Create a remote repository on GitHub, link your local repository to GitHub, and push your code.

```bash
git remote add origin https://github.com/your-git-username/MarketPeak_Ecommerce.git
git push -u origin main
```

### 2. AWS Deployment

#### 2.1. Set Up an AWS EC2 Instance

Log in to the AWS Management Console, launch an EC2 instance using Amazon Linux AMI, and connect to the instance using SSH.

#### 2.2. Clone the repository on the Linux Server

Clone the GitHub repository to your AWS EC2 instance using SSH or HTTPS methods.

SSH Method:

```bash
ssh-keygen
cat /home/ubuntu/.ssh/id_rsa.pub
git clone git@github.com:yourusername/MarketPeak_Ecommerce.git
```

HTTPS Method:

```bash
git clone https://github.com/yourusername/MarketPeak_Ecommerce.git
```

#### 2.3. Install a Web Server on EC2

Install Apache HTTP Server on the EC2 instance and start the service.

```bash
sudo yum update -y
sudo yum install httpd -y
sudo systemctl start httpd
sudo systemctl enable httpd
```

#### 2.4. Configure httpd for Website

Clear the default httpd web directory, copy your website files to it, and reload httpd service.

```bash
sudo rm -rf /var/www/html/*
sudo cp -r ~/MarketPeak_Ecommerce/* /var/www/html/
sudo systemctl reload httpd
```

#### 2.5. Access Website from Browser

Access your deployed website using the public IP or URL of your EC2 instance in a web browser.

Public IP: `xx.xx.xx.xx`

URL: `http://xx.xx.xx.xx`

### 3. Continuous Integration and Deployment Workflow

Follow a structured workflow for developing, testing, and deploying updates to your e-commerce platform using Git and AWS.

- **Step 1:** Develop new features and fixes in a development branch.
- **Step 2:** Stage, commit, and push changes to GitHub.
- **Step 3:** Create pull requests for code review and merge changes into the main branch.

### 4. Documenting the Deployment Process

Here is a detailed documentation of the steps taken to deploy the "MarketPeak_Ecommerce" platform using Git, Linux, and AWS, including any troubleshooting or challenges faced and their solutions.

#### Troubleshooting and Solutions

1. **SSH Connection to EC2 Instance:**

   - **Issue:** Initially faced difficulty connecting to the EC2 instance via SSH.
   - **Solution:** Ensured that the security group associated with the EC2 instance allowed SSH access from my IP address. Generated SSH keypair using `ssh-keygen` and added the public key to the EC2 instance for authentication.

2. **HTTPD Configuration for Website:**

   - **Issue:** The website was not loading correctly after copying files to the httpd directory.
   - **Solution:** Checked httpd error logs (`/var/log/httpd/error_log`) for any issues. Discovered that permissions were not set correctly on some files. Used `chmod` and `chown` commands to adjust permissions and ownership of files in the httpd directory.

3. **HTTPS Clone vs. SSH Clone:**

   - **Issue:** Confusion regarding whether to use HTTPS or SSH for cloning the GitHub repository on the EC2 instance.
   - **Solution:** Decided to use SSH for cloning as it provides a more secure and authenticated connection to GitHub. Generated SSH keypair on the EC2 instance and added the public key to GitHub for authentication.

4. **Continuous Integration and Deployment Workflow:**
   - **Issue:** Ensuring a smooth workflow for developing, testing, and deploying updates to the platform.
   - **Solution:** Established a structured workflow using Git branches (development branch for new features and fixes, main branch for production-ready code). Utilized pull requests on GitHub for code review and merging changes into the main branch.

### Conclusion

The deployment process for the "MarketPeak_Ecommerce" platform involved setting up version control with Git, developing in a Linux environment, and deploying on an AWS EC2 instance. By following the outlined steps and addressing any challenges encountered, the platform was successfully deployed and made accessible to users.

---
