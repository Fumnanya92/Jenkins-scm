# Jenkins Job Project

In Jenkins, a job is a unit of work or a task that can be executed by the Jenkins automation server.

A Jenkins job represents a specific task or set of tasks that needs to be performed as part of a build or deployment process. Jobs in Jenkins are created to automate the execution of various steps such as compiling code, running tests, packaging applications, and deploying them to servers. Each Jenkins job is configured with a series of build steps, post-build actions, and other settings that define how the job should be executed.

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

As engineers, we need to be able to automate tasks and make our work easier in every possible way. We have connected Jenkins to the `jenkins-scm` repository, but currently, we cannot run a new build without clicking on **Build Now**. To eliminate this, we need to configure a build trigger in our Jenkins job. With this, Jenkins will automatically run a new build whenever a change is made to our GitHub repository.

1. Click on **Configure** for your job and add the following configurations.
2. Click on **Build Triggers** to configure triggering the job from a GitHub webhook.
3. **Create a GitHub webhook** using the Jenkins IP address and port.


#Jenkins Pipline


