# 🚀Jenkins Pipeline with GitHub Webhook

This project demonstrates how to set up a Jenkins Declarative Pipeline using GitHub as the SCM (Source Control Management) and automatically trigger builds via GitHub Webhooks.

# 🚀 Features

Uses Jenkins Declarative Pipeline

Triggers builds automatically when code is pushed to GitHub

Uses GitHub Webhooks for automation

Secure authentication via SSH keys or GitHub Token

Works with ngrok to expose Jenkins to GitHub

# 📌 Prerequisites

Ensure you have the following installed and configured:

Jenkins (with Git & Pipeline plugins installed)

GitHub Account

Ngrok (for exposing Jenkins if hosted locally)

SSH key or GitHub token for authentication

#🔧 Setup Instructions

1️⃣ Create a GitHub Repository
Create a new repository on GitHub.

Add a Jenkinsfile at the root of the repository.

2️⃣ Configure SSH Key (if using SSH URL)

ssh-keygen -t rsa -b 4096 -C "your-email@example.com"

cat ~/.ssh/id_rsa.pub

Copy the output and go to GitHub → Settings → SSH and GPG Keys → New SSH Key.

Paste the copied key and save.

3️⃣ Configure Jenkins Credentials for GitHub

Go to Jenkins Dashboard → Manage Jenkins → Credentials → Add Credentials.

Select SSH Username with private key and enter your private key path.

If using HTTPS, use GitHub Token instead.

4️⃣ Configure GitHub Webhook

Start ngrok to expose Jenkins:

ngrok http 8080

Copy the ngrok forwarding URL (e.g., https://xyz.ngrok-free.app).

Go to GitHub → Your Repository → Settings → Webhooks.

Click Add Webhook and set:

Payload URL: https://xyz.ngrok-free.app/github-webhook/

Content type: application/json

Trigger: Just the push event

5️⃣ Create a Jenkins Pipeline

In Jenkins, create a new pipeline job.

Set Pipeline script from SCM → Git and enter your repository URL.

Specify the branch (main or master).

Click Save and Build Now to test.

🛠 Sample Jenkinsfile

pipeline {
    agent any
    stages {
        stage('Clone Repo') {
            steps {
                git 'git@github.com:your-username/your-repo.git'
            }
        }
        stage('Build') {
            steps {
                echo "Building..."
            }
        }
        stage('Test') {
            steps {
                echo "Running tests..."
            }
        }
        stage('Deploy') {
            steps {
                echo "Deploying application..."
            }
        }
    }
}

🎯 Testing the Webhook

Make any change to your GitHub repo and push it:

git add .
git commit -m "Testing webhook trigger"
git push origin main

Jenkins should automatically trigger a new build.

Check Jenkins Dashboard → Your Job → Build History for the latest run.

🔍 Troubleshooting
If webhook doesn't trigger, check GitHub → Webhooks → Recent Deliveries for errors.

Ensure ngrok is running and using the correct URL in the webhook.

If SSH fails, ensure your public key is added to GitHub and the private key is in Jenkins credentials.

# ✨ Conclusion

This project is fully functional. Every push to GitHub **automatically triggers a Jenkins pipelinethat builds, tests, and deploys the application. 

Now, every time you push code to GitHub, Jenkins will automatically build, test, and deploy your project! 🎉🚀

