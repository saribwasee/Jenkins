// 
pipeline { 
    agent any 

    tools { 
        maven 'maven-3.9' 
        // Use the configured Maven tool named 'maven-3.9' as defined in Jenkins global tool configuration
    }

    stages {
        stage('Git') {
            steps {
                echo "Getting the application"
                // Cloning the Git repository and checking out the specified branch
                git branch: 'bugfix/jenkins-pipeline', url: 'https://gitlab.com/nanuchi/java-maven-app.git'
            }
        }

        stage('Build') {
            steps {
                echo "Building the application"
                // Running the Maven package command to build the application
                sh "mvn package"
            }
        }

        stage('Push') {
            steps {
                echo "Pushing the application"
                // Using Docker Hub credentials to build, login, and push the Docker image
                withCredentials([usernamePassword(credentialsId: 'dockerhub-ID', passwordVariable: 'PASSWORD', usernameVariable: 'USERNAME')]) {
                    // Building the Docker image with the specified tag
                    sh "docker build -t saribwasee/demo-app:jma-1.0 ."
                    // Logging into Docker Hub using the provided credentials
                    sh "echo $PASSWORD | docker login -u $USERNAME --password-stdin"
                    // Pushing the Docker image to Docker Hub
                    sh "docker push saribwasee/demo-app:jma-1.0" 
                }
            }
        }
    }
}
