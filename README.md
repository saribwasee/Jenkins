# Jenkins


Jenkins is an open source automation server. It helps automate the parts of software development related to building, testing, and deploying, facilitating continuous integration, and continuous delivery. It is a server-based system that runs in servlet containers such as Apache Tomcat. 

In Jenkins, a build trigger is a mechanism that initiates the execution of a Jenkins job or pipeline. Triggers are used to start builds automatically based on various events or conditions. There are several ways to trigger builds in Jenkins: which can be configured


## Jenkins Build Triggers

- Manual Build Trigger:
Build Now: You can manually trigger a build at any time by clicking the “Build Now” or “Build” button on the Jenkins dashboard for a specific job.

- Scheduled Build Trigger:
Build Periodically: You can schedule builds to run at specific intervals using the “Build periodically” option in the job configuration

- SCM (Source Code Management) Trigger:
Poll SCM: If you’re using a version control system (e.g., Git, Subversion), you can configure the job to poll the repository for changes. When changes are detected, Jenkins will automatically trigger a build.


- Webhooks Trigger: Many version control systems and external services support webhooks, which allow them to notify Jenkins when code changes occur.


- Dependency Build Trigger: Build after other projects are built: You can configure a job to be triggered after one or more upstream jobs have been built successfully

- Parameterized Build Trigger: You can set up parameterized builds where a build is triggered with specific parameter values. 

- Pipeline Trigger: If you’re using Jenkins Pipelines (defined in a Jenkinsfile), you can use various triggers within the pipeline script itself. For example, you can set up a webhook trigger, a schedule trigger, or a manual input trigger as part of your pipeline script.

- Remote API Trigger: You can trigger Jenkins builds remotely using its REST API. This allows you to programmatically initiate builds from external scripts or applications.

- Plugin-Based Triggers: Jenkins has numerous plugins available that can provide additional trigger mechanisms. For example, the “GitHub Webhook” plugin allows Jenkins to listen to GitHub events and trigger builds accordingly.




- We installing jenkins on docker container

```bash
 docker run -p 8080:8080 -p 50000:50000 -d -v jenkins_home:/var/jenkins_home jenkins/jenkins:lts 
```

```bash
docker run -p 8080:8080 -p 50000:50000 -d -v jenkins_home:/var/jenkins_home -v /var/run/docker.sock:/var/run/docker.sock -v $(which docker):/usr/bin/docker jenkins/jenkins:lts
```

```bash 
docker volume inspect jenkins_home
```


In global configuration we can adding tools so we can use it in our projects and we can install tools on cli or install plugins on jenkins portal


freestyle jobs are GUI where we can add plugins from tools then use it to from jobs 

For Package

1.	Install plugins and add in global configuration tools then use it to jobs 


In pipeline we use scripting groovy language 

Here is sample 

```bash

pipeline { agent any

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


Similarly multi branch pipline use the same script with all individual pipelines

### For trigger alert we need to sync Jenkins to Gitlab  (gitlab plugin)

Addin in configuration Jenkins

![image](https://github.com/user-attachments/assets/4a80f908-e9f3-4dc0-9765-e253b8ee1f8e)

 
For API tokens go to gitlab in option preferences there will be access token 
 
![image](https://github.com/user-attachments/assets/b32c22ed-a6ed-4a6d-9f35-847528b0bc33)


Then copy the generated code (it wouldn’t never show again)
Then we can add it from the pipeline
Again go to gitlab then setting > integration tab 
Jenkins CI (Enable integration – mark check on push trigger )

![image](https://github.com/user-attachments/assets/c81f3129-63ee-4505-ba2e-f8f67d391004)

 
Now we can use it from git repo 




Complete pipeline but without trigger update made and tested

```bash
pipeline { agent any tools { maven 'maven-3.9' // Ensure 'Maven' matches exactly with Jenkins configuration }
    stages {
        stage('Git') {
            steps {
        echo "Getting the application"
        // Correct command to clone and checkout a specific branch
        git branch: 'bugfix/jenkins-pipeline', url: 'https://gitlab.com/nanuchi/java-maven-app.git'
    }
}

    stage('Build') {
            steps {
        echo "Building the application"
        sh "mvn package"
    }
}
    stage('Push') {
            steps {
        echo "Pushing the application"
        withCredentials([usernamePassword(credentialsId: 'dockerhub-ID', passwordVariable: 'PASSWORD', usernameVariable: 'USERNAME')]) {
            sh "docker build -t saribwasee/demo-app:jma-1.0 ."
            sh "docker login -u $USERNAME -p $PASSWORD"
            sh "docker push saribwasee/demo-app:jma-1.0"
        }
    }
}
} }

```


