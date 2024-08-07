# Jenkins

Jenkins is an open source automation server that helps automate parts of software development related to building, testing, and deploying, facilitating continuous integration and continuous delivery. It is a server-based system that runs in servlet containers such as Apache Tomcat. 

In Jenkins, a build trigger is a mechanism that initiates the execution of a Jenkins job or pipeline. Triggers are used to start builds automatically based on various events or conditions. Here are several ways to trigger builds in Jenkins:

## Jenkins Build Triggers

- **Manual Build Trigger:**
  - **Build Now:** You can manually trigger a build at any time by clicking the “Build Now” or “Build” button on the Jenkins dashboard for a specific job.

- **Scheduled Build Trigger:**
  - **Build Periodically:** Schedule builds to run at specific intervals using the “Build periodically” option in the job configuration.

- **SCM (Source Code Management) Trigger:**
  - **Poll SCM:** If you’re using a version control system (e.g., Git, Subversion), configure the job to poll the repository for changes. Jenkins will automatically trigger a build when changes are detected.

- **Webhooks Trigger:** Many version control systems and external services support webhooks, allowing them to notify Jenkins when code changes occur.

- **Dependency Build Trigger:** 
  - **Build after other projects are built:** Configure a job to be triggered after one or more upstream jobs have been built successfully.

- **Parameterized Build Trigger:** Set up parameterized builds where a build is triggered with specific parameter values.

- **Pipeline Trigger:** If you’re using Jenkins Pipelines (defined in a Jenkinsfile), use various triggers within the pipeline script itself. For example, set up a webhook trigger, a schedule trigger, or a manual input trigger as part of your pipeline script.

- **Remote API Trigger:** Trigger Jenkins builds remotely using its REST API. This allows you to programmatically initiate builds from external scripts or applications.

- **Plugin-Based Triggers:** Jenkins has numerous plugins available that can provide additional trigger mechanisms. For example, the “GitHub Webhook” plugin allows Jenkins to listen to GitHub events and trigger builds accordingly.

## Installing Jenkins on Docker

To install Jenkins on a Docker container, use the following commands:

```bash
docker run -p 8080:8080 -p 50000:50000 -d -v jenkins_home:/var/jenkins_home jenkins/jenkins:lts 
```

If we need docker in inside the jenkins 

```bash
docker run -p 8080:8080 -p 50000:50000 -d -v jenkins_home:/var/jenkins_home -v /var/run/docker.sock:/var/run/docker.sock -v $(which docker):/usr/bin/docker jenkins/jenkins:lts
```

To inspect the Docker volume:

```bash
docker volume inspect jenkins_home
```

In the global configuration, you can add tools to use in your projects. You can install tools on the CLI or install plugins via the Jenkins portal.

Freestyle jobs are GUI-based where you can add plugins from tools and then use them in jobs. 

## Package Installation

1. Install plugins and add them in global configuration tools, then use them in jobs.

## Pipeline Scripting

In Jenkins Pipelines, we use Groovy scripting language. Here is a sample pipeline script:

```groovy
pipeline { 
    agent any

    stages {
        stage('Build') {
            steps {
                echo "Building the application"
            }
        }
        stage('Test') {
            steps {
                echo "Testing the application"
            }
        }
        stage('Push') {
            steps {
                echo "Pushing the application"
            }
        }
    }
}
```
