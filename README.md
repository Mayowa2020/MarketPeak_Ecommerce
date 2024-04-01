# MarketPeak E-Commerce Platform

Welcome to the MarketPeak E-Commerce Platform! This project aims to create a robust and user-friendly online marketplace where users can explore product listings, add items to their shopping cart, and enjoy secure user authentication. To achieve this, we'll utilize Git for version control, develop the platform in a Linux environment, and deploy it on an AWS EC2 instance.

## Table of Contents

1. [Getting Started](#getting-started)
   - [Version Control with Git](#version-control-with-git)
   - [Obtaining and Preparing the Website Template](#obtaining-and-preparing-the-website-template)
   - [Customization](#customization)
2. [Deployment](#deployment)
3. [Continuous Integration and Deployment Workflow](#continuous-integration-and-deployment-workflow)
4. [Troubleshooting and Solutions](#troubleshooting-and-solutions)

5. [License](#license)

## Getting Started

### Version Control with Git

Let’s kick off our project by setting up Git for version control. Follow these steps:

### 1. Initialize Git Repository

1. Create a project directory named "MarketPeak_Ecommerce":

   ```bash
   mkdir MarketPeak_Ecommerce
   cd MarketPeak_Ecommerce
   ```

2. Initialize a Git repository to manage version control:

   ```bash
   git init
   ```

### 2. Obtaining and Preparing the Website Template

- Instead of building the website from scratch, we’ll use a pre-existing e-commerce website template. This allows us to focus on deployment and operational aspects.
- Download a suitable e-commerce website template from resources like Tooplate or other free template providers.
- Extract the downloaded template into your project directory, `MarketPeak_Ecommerce`.

### 3. Stage and Commit the Template to Git

1. **Add Your Website Files:**

   - Place all your e-commerce website template files inside the `MarketPeak_Ecommerce` directory.
   - In your terminal, navigate to the project directory:

     ```bash
     cd MarketPeak_Ecommerce
     ```

   - Add the files to the Git staging area:

     ```bash
     git add .
     ```

2. **Set Your Git Global Configuration:**

   - Configure your Git username and email globally (replace with your actual details):

     ```bash
     git config --global user.name "YourUsername"
     git config --global user.email "youremail@example.com"
     ```

3. **Commit Your Changes:**
   - Commit your changes with a clear, descriptive message:

     ```bash
     git commit -m "Initial commit with basic e-commerce site structure"
     ```

## Deployment

Our next step is deploying the platform on an AWS EC2 instance. Follow these steps:

### 1. Set Up an AWS EC2 Instance

1. Log in to the [AWS Management Console](https://aws.amazon.com/console/).
2. Launch an EC2 instance using an Amazon Linux AMI.
3. Connect to the instance using SSH.

### 2. Clone the Repository on the Linux Server

Before deploying your e-commerce platform, you'll need to clone the GitHub repository to your AWS EC2 instance. You have two primary methods for cloning a repository: SSH and HTTPS.

#### SSH Method

1. On your EC2 instance, generate an SSH key pair using `ssh-keygen`.
2. Display and copy your public key:

   ```bash
   cat /home/ubuntu/.ssh/id_rsa.pub
   ```

3. Add the SSH public key to your GitHub account.
4. Use the SSH clone URL to clone the repository:

   ```bash
   git clone git@github.com:yourusername/MarketPeak_Ecommerce.git
   ```

#### HTTPS Method

For repositories where you don't want to set up SSH keys, use the HTTPS URL. GitHub will prompt you for your username and password:

```bash
git clone https://github.com/yourusername/MarketPeak_Ecommerce.git
```

### 3. Install a Web Server on EC2

The Apache HTTP Server (httpd) is widely used for serving HTML files and content over the internet. Let's install it on your Linux EC2 instance to host the MarketPeak E-commerce site:

1. Update the package manager:

   ```bash
   sudo yum update -y
   ```

2. Install Git (if not already installed):

   ```bash
   sudo yum install git -y
   ```

3. Install Apache web server:

   ```bash
   sudo yum install httpd -y
   ```

4. Start the Apache service:

   ```bash
   sudo systemctl start httpd
   ```

5. Enable the Apache service to start on boot:

   ```bash
   sudo systemctl enable httpd
   ```

### 4. Configure httpd for the Website

To serve the website from the EC2 instance, configure httpd to point to the directory where the website code files are stored (usually `/var/www/html`):

1. **Prepare the Web Directory:**

   - Clear the default httpd web directory:

     ```bash
     sudo rm -rf /var/www/html/*
     ```

   - Copy the MarketPeak E-commerce website files to it:

     ```bash
     sudo cp -r ~/MarketPeak_Ecommerce/* /var/www/html/
     ```

2. **Reload httpd:**
   Apply the changes by reloading the httpd service:

   ```bash
   sudo systemctl reload httpd
   ```

### 5. Access the Website from Your Browser

With httpd configured and the website files in place, the MarketPeak E-commerce platform is now live on the internet:

1. Open a web browser.
2. Access the public IP address of your EC2 instance to view the deployed website.



## Continuous Integration and Deployment Workflow

To ensure a smooth workflow for developing, testing, and deploying your e-commerce platform, follow this structured approach. It covers making changes in a development environment, utilizing version control with Git, and deploying updates to your production server on AWS.

### Step 1: Developing New Features and Fixes

1. **Create a Development Branch:**

   - Begin your development work by creating a separate branch. This isolates new features and bug fixes from the stable version of your website.

     ```bash
     git branch development
     git checkout development
     ```

2. **Implement Changes:**

   - On the development branch, add your new features or bug fixes. This might include updating web pages, adding new products, or fixing known issues.

### Step 2: Version Control with Git

1. **Stage Your Changes:**

   - After making your changes, add them to the staging area in Git. This prepares the changes for a commit.

     ```bash
     git add .
     ```

2. **Commit Your Changes:**

   - Securely save your changes in the Git repository with a commit. Include a descriptive message about the updates.

     ```bash
     git commit -m "Add new features or fix bugs"
     ```

3. **Push Changes to GitHub:**

   - Upload your development branch with the new changes to GitHub. This enables collaboration and version tracking.

     ```bash
     git push origin development
     ```

### Step 3: Pull Requests and Merging to the Main Branch

1. **Create a Pull Request (PR):**

   - On GitHub, create a pull request to merge the development branch into the main branch. This process is crucial for code review and maintaining code quality.

2. **Review and Merge the PR:**

   - Review the changes for any potential issues. Once satisfied, merge the pull request into the main branch, incorporating the new features or fixes into the production codebase.

     ```bash
     git checkout main
     git merge development
     ```

3. **Push the Merged Changes to GitHub:**

   - Ensure that your local main branch, now containing the updates, is pushed to the remote repository on GitHub.

     ```bash
     git push origin main
     ```

## Troubleshooting and Solutions

1. **SSH Connection to EC2 Instance:**

   - **Issue:** Initially faced difficulty connecting to the EC2 instance via SSH.
   - **Solution:** Ensured that the security group associated with the EC2 instance allowed SSH access from my IP address. Generated an SSH key pair using `ssh-keygen` and added the public key to the EC2 instance for authentication.

2. **HTTPD Configuration for Website:**

   - **Issue:** Encountered website loading issues after copying files to the httpd directory.
   - **Solution:** Checked httpd error logs (`/var/log/httpd/error_log`) for any issues. Discovered that permissions were not set correctly on some files. Used `chmod` and `chown` commands to adjust permissions and ownership of files in the httpd directory.

3. **HTTPS Clone vs. SSH Clone:**

   - **Issue:** Confusion regarding whether to use HTTPS or SSH for cloning the GitHub repository on the EC2 instance.
   - **Solution:** Opted to use SSH for cloning as it provides a more secure and authenticated connection to GitHub. Generated an SSH key pair on the EC2 instance and added the public key to GitHub for authentication.

4. **Continuous Integration and Deployment Workflow:**

   - **Issue:** Ensuring a smooth workflow for developing, testing, and deploying updates to the platform.
   - **Solution:** Established a structured workflow using Git branches (development branch for new features and fixes, main branch for production-ready code). Utilized pull requests on GitHub for code review and merging changes into the main branch.


## Conclusion

The deployment process for the "MarketPeak_Ecommerce" platform involved setting up version control with Git, developing in a Linux environment, and deploying on an AWS EC2 instance. By following the outlined steps and addressing any challenges encountered, the platform was successfully deployed and made accessible to users.


## License

This project is licensed under the [MIT License](LICENSE), which means you can freely use and modify the code as per the license terms.

---

Thank you for choosing MarketPeak E-Commerce Platform for your online marketplace needs. If you have any questions or need further assistance, please don't hesitate to reach out. Happy coding! 🛒🚀
```
