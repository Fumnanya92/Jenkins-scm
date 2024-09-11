Here’s your step-by-step Jenkins project documentation in Markdown format for GitHub:

```markdown
# Jenkins Job Project

In Jenkins, a job is a unit of work or a task that can be executed by the Jenkins automation server.

A Jenkins job represents a specific task or set of tasks that need to be performed as part of a build or deployment process. Jobs in Jenkins are created to automate the execution of various steps such as compiling code, running tests, packaging applications, and deploying them to servers. Each Jenkins job is configured with a series of build steps, post-build actions, and other settings that define how the job should be executed.

## Creating a Freestyle Project

### Let's create our first build job

1. From the dashboard menu on the left side, click on **New Item**.

## Connecting Jenkins to Our Source Code Management

### Jenkins Freestyle Project

Now that we have created a freestyle project, let's connect Jenkins with GitHub.

1. **Create a new GitHub repository** called `jenkins-scm` with a `README.md` file.
2. **Connect Jenkins** to the `jenkins-scm` repository by pasting the repository URL in the appropriate field. Ensure your current branch is `main`.
3. **Save the configuration** and run **Build Now** to connect Jenkins to our repository.

## Configuring Build Trigger

As engineers, we need to automate tasks to make our work easier. We have connected Jenkins to the `jenkins-scm` repository, but we cannot run a new build without clicking **Build Now**. To automate this process, we need to configure a build trigger. This way, Jenkins will automatically run a new build whenever changes are made to our GitHub repository.

1. Click on **Configure** for your job and add the following configurations.
2. Click on **Build Triggers** to configure triggering the job from a GitHub webhook.
3. **Create a GitHub webhook** using the Jenkins IP address and port.

---

# Jenkins Pipeline Project

## What is a Jenkins Pipeline Job?

A Jenkins pipeline job is a way to define and automate a series of steps in the software delivery process. It allows you to script and organize your entire build, test, and deployment pipeline. Jenkins pipelines enable organizations to define, visualize, and execute complex build, test, and deployment processes of code. This integrates continuous integration and continuous delivery (CI/CD) practices into software development.

Let's recall our Docker Foundations project, where we created a Dockerfile and made a Docker image and container with it. Now, let's automate the same process using Jenkins pipeline code.

### Creating a Pipeline Job

1. From the dashboard menu on the left side, click on **New Item**.
2. Create a pipeline job and name it **My pipeline job**.

### Configuring Build Trigger

Create a build trigger for Jenkins to trigger new builds:

1. Click **Configure** for your job and add the necessary configurations.
2. Create a webhook on GitHub for Jenkins.

### Writing Jenkins Pipeline Script

A Jenkins pipeline script defines and orchestrates the steps and stages of a CI/CD pipeline. Jenkins pipelines can be defined using either **Declarative** or **Scripted** syntax. Declarative syntax is more structured and concise, while scripted syntax provides more flexibility for complex scripting needs.

#### Let's write our pipeline script:

```groovy
pipeline {
    agent any

    stages {
        stage('Connect To GitHub') {
            steps {
                checkout scmGit(branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/Fumnanya92/jenkins-scm.git']])
            }
        }
        stage('Build Docker Image') {
            steps {
                script {
                    sh 'docker build -t dockerfile .'
                }
            }
        }
        stage('Run Docker Container') {
            steps {
                script {
                    sh 'docker run -itd -p 8081:80 dockerfile'
                }
            }
        }
    }
}
```

**Copy the Pipeline script and paste it into the pipeline script section.**

---

## Installing Docker

Before Jenkins can run Docker commands, we need to install Docker on the same instance where Jenkins is installed. Using shell scripting, let's install Docker:

### Steps:

1. Create a file named `docker.sh`.
2. Open the file and paste the script below:
   ```bash
   sudo apt-get update -y
   sudo apt-get install ca-certificates curl gnupg
   sudo install -m 0755 -d /etc/apt/keyrings
   curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg
   sudo chmod a+r /etc/apt/keyrings/docker.gpg

   # Add the repository to Apt sources:
   echo \
     "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.gpg] https://download.docker.com/linux/ubuntu \
     $(. /etc/os-release && echo "$VERSION_CODENAME") stable" | \
     sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
   sudo apt-get update -y
   sudo apt-get install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin -y
   sudo systemctl status docker
   ```
3. Save and close the file.
4. Make the file executable:
   ```bash
   chmod u+x docker.sh
   ```
5. Execute the `docker.sh` script:
   ```bash
   ./docker.sh
   ```

---

## Building Pipeline Script

Now that Docker is installed, we need to create a Dockerfile before we can run our pipeline script. As we know, we cannot build a Docker image without a Dockerfile.

### Steps:

1. Create a new file named **Dockerfile**.
2. Paste the code snippet below in the file:
   ```Dockerfile
   # Use the official NGINX base image
   FROM nginx:latest

   # Set the working directory in the container
   WORKDIR  /usr/share/nginx/html/

   # Copy the local HTML file to the NGINX default public directory
   COPY index.html /usr/share/nginx/html/

   # Expose port 80 to allow external access
   EXPOSE 80
   ```
3. Create an **index.html** file and paste the following content:
   ```html
   Congratulations, You have successfully run your first pipeline code.
   ```

Pushing the Dockerfile and index.html file will automatically trigger Jenkins to run a new build for the pipeline.

To access the content of the **index.html** file on a web browser, edit inbound rules and open the port we mapped our container to (8081).
```

You can directly use this for your GitHub documentation. Let me know if you need any changes!
