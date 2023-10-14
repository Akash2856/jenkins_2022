# Jenkins Installation and CI/CD Setup on Amazon Linux

This guide outlines the steps to install Jenkins on Amazon Linux and configure two Jenkins jobs: "git_hub" for continuous deployment from GitHub and "setupwebserver" for setting up an Apache web server.

## Jenkins Installation

1. **SSH into your Amazon Linux instance.**

2. **Install Java:**

   ```bash
   sudo yum install java-1.8.0-openjdk-devel -y

## Jenkins Job "git_hub"

1. **Create a new Jenkins job named "git_hub."**

2. **Configure the job as follows:**

   - Use the "GitHub Pull Request" plugin.
   - Set the repository URL and credentials.

3. **In the "Build" section, add a build step to copy the code from `/var/lib/jenkins/workspace/JOB_NAME` to `/var/www/html`. This step will deploy your code to the Apache web server for hosting.

4. **Use "Poll SCM" in the job configuration to deploy code automatically on GitHub pushes. With this setup, Jenkins will monitor your GitHub repository for changes, and when new code is pushed, it will automatically trigger the deployment process.

This Jenkins job, "git_hub," is responsible for continuous deployment from your GitHub repository to the Apache web server. It automates the process of updating your website whenever there are new code changes on GitHub.

![image](https://github.com/Akash2856/jenkins_2023/assets/49570016/29d2f978-2c0c-4846-a109-65b8bddfde00)
![image](https://github.com/Akash2856/jenkins_2023/assets/49570016/8919efc4-e3f7-432e-9a07-099b6685d204)
![image](https://github.com/Akash2856/jenkins_2023/assets/49570016/d2a4b36e-4f09-4798-8933-3df67e562cfb)


## Jenkins Job "setupwebserver"

1. **Create a new Jenkins job named "setupwebserver."**

2. **Enable Jenkins to run system-level commands:**

   - To give Jenkins root-level power, add the following line to the `/etc/sudoers` file:

     ```bash
     jenkins ALL=(ALL) PASSWD: ALL
     ```
     ![image](https://github.com/Akash2856/jenkins_2023/assets/49570016/8300ae0d-3221-4eea-8d95-630d2755018f)


3. **In the job configuration, use the "Execute Shell" build step to install and start the Apache HTTPD server. The following commands can be used:

   ```bash
   sudo yum install httpd -y
   sudo systemctl start httpd
