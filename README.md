➡️Name- Piyush, Batch-BCA PPU 3rd year, ID-444-5031
🚀 Day 1: Git, AWS EC2, and GitHub Actions Setup
1. Git Repository Setup and Initial Commit
This section covers initializing your project and pushing the initial development code to your new GitHub repository.
Initial Git Configuration (First-Time Use)
If this is your first time using Git on this machine, you must configure your identity:
Command	Purpose
git config --global user.name "YOUR USERNAME"	Sets your user name for all future commits.
git config --global user.email "YOUR EMAIL"	Sets your email for all future commits.
Code Setup and Push
1.	Create Repository: Create a new Git repository on a platform like GitHub (e.g., your-repo-name). Obtain the URL of the created repository.
2.	Local Folder Creation: Create a new folder on your local machine.
3.	Clone Repository: Open Git Bash inside the new folder and clone the repository:
Bash
git clone <URL_OF_YOUR_REPO>
4.	Add Development Code: Navigate into the newly cloned repository directory:
Bash
cd your-repo-name
Paste all of your development code files into this directory.
5.	Check Status: Check which files are untracked:
Bash
git status
6.	Stage Files: Add all changes (new and modified files) to the staging area:
Bash
git add .
7.	Check Status Again: Verify that all files are staged for commit:
Bash
git status
8.	Commit Changes: Commit the staged files with a descriptive message:
Bash
git commit -m "Initial commit of development code"
9.	Push Code: Push the committed changes to the remote repository:
Bash
git push
You will now see your code in the online repository.
________________________________________
2. AWS EC2 Instance Creation
This section details launching a new virtual machine (EC2 instance) on Amazon Web Services.
1.	Go to AWS Console: Log in to your AWS Management Console.
2.	Search and Launch: Search for EC2 and click Launch Instance.
3.	Configure Instance:
o	Name: Give your instance a recognizable name (e.g., DevOps-App-Server).
o	Application and OS Images (AMI): Select the desired image file (e.g., Ubuntu Server for free tier).
o	Instance Type: Select a free-tier eligible instance type (e.g., t2.micro).
4.	Key Pair (Login): This is essential for accessing your instance via SSH.
o	Choose an existing key pair or create a new key pair.
o	If creating new:
	Give it a name.
	Choose RSA or ED25519 as the key pair type.
	Select the format: .pem (for OpenSSH/Linux) or .ppk (for PuTTY/Windows).
o	Click Create key pair. The key file (e.g., your-keypair-name.pem) will automatically download. This file is your access key.
5.	Network Settings: Ensure the Security Group allows SSH traffic (Port 22) from your IP or everywhere.
6.	Storage: Select the appropriate volume size (default free-tier limits are usually sufficient).
7.	Launch Instance: Click Launch instance. Your EC2 machine will be created.
Accessing EC2 from Command Line
1.	Locate Key: Open your command prompt/terminal and navigate to the folder where your .pem key pair file was downloaded.
2.	SSH Command: Get the Public IP address of your running EC2 instance from the AWS console. Use the following command to connect (assuming an Ubuntu AMI):
Bash
ssh -i your-keypair-name.pem ubuntu@<PUBLIC_IP_OF_EC2>
Hit Enter to establish the secure connection.
________________________________________
3. GitHub Actions Secrets Configuration
To allow your GitHub Actions workflow (which will be defined in a separate YAML file) to connect and deploy code to your AWS EC2 instance, you need to securely store the connection details as repository secrets.
1.	Go to GitHub Repository: Open your created repository on GitHub.
2.	Navigate to Secrets:
o	Click on Settings.
o	In the left sidebar, go to Security $\rightarrow$ Secrets and variables.
o	Click on Actions.
3.	Add Repository Secrets: Click New repository secret three times to create the necessary secrets.
Secret Name	Secret Value	Description
EC2_HOST	The Public IP or Public DNS of your EC2 instance.	The address to connect to.
EC2_USER	The username for SSH access, usually ubuntu.	The login user name.
EC2_SSH_KEY	The entire contents of your private .pem key file.	The private key needed for authentication.
•	To get the EC2_SSH_KEY value: Open your .pem file with a text editor (like VS Code or Notepad) and copy the entire content, including the -----BEGIN... and -----END... lines, and paste it as the secret value.
________________________________________
4. Checking GitHub Actions
After configuring the secrets, any subsequent step involving the GitHub Action workflow (usually triggered by pushing a YAML file named main.yml or similar to the .github/workflows directory) will use these secrets.
1.	Check Actions Tab: Click on the Actions tab in your repository.
2.	Review Workflows: Once you have a workflow file, you will see the action runs listed here, which you can check for success or failure.

