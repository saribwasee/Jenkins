
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
}
}
