


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


# Jenkins: Freestyle Projects vs Pipeline Jobs

The main difference I see between Jenkins Freestyle projects and Pipeline is the usage of GUI vs scripting

## Freestyle jobs 

- GUI-based where you can add plugins from tools and then use them in jobs by installing Package (Install plugins and add them in global configuration tools, then use them in jobs.)
  -  In the global configuration, you can add tools to use in your projects. You can install tools on the CLI or install plugins via the Jenkins portal.

## Freestyle Projects
- **Use GUI**: Add different stages and steps using a graphical user interface.
- **Suitable for Less Complex Scenarios**: Ideal for simpler projects or those new to Jenkins/CI solutions.
- **Beginner-Friendly**: Easy to set up and understand.
- **Limitations**: Can become difficult to manage and achieve desired results as scenarios grow in complexity.

## Pipeline Jobs
- **Use Code**: Utilize Groovy language (similar to Java) for defining instructions.
- **Version Control**: Since everything is in one script, it can be kept in source control, allowing for version tracking and rollback capabilities.
- **Comprehensive Steps**: Entire pipeline consists of steps such as build, test, deploy, etc.
- **Jenkinsfile**: Pipelines are created using a Jenkinsfile, which can be stored in a git repository.
- **Pipeline Types**:
  - **Declarative Pipeline**: Always begins with `pipeline` and breaks down into stages that contain multiple steps.
  - **Scripted Pipeline**: Begins with `node` and uses Groovy code, referencing Jenkins Pipeline DSL (Domain Specific Language) with stage elements (without needing steps).




In Jenkins Pipelines, we use Groovy scripting language. Here is a sample pipeline script:

## Scripted Pipeline Example

```groovy
node {
    stage('Build') {
        script {
            echo "Building the application..."
        }
    }

    stage('Test') {
        script {
            echo "Testing the application..."
        }
    }

    stage('Deploy') {
        script {
            echo "Deploying the application..."
        }
    }
}
```

### Declarative Pipeline Example

```groovy
pipeline {
    agent none
    stages {
        stage('build') {
            steps {
                script {
                    echo "Building the application..."
                }
            }
        }
        stage('test') {
            steps {
                script {
                    echo "Testing the application..."
                }
            }
        }
        stage('deploy') {
            steps {
                script {
                    echo "Deploying the application..."
                }
            }
        }
    }
}
```
