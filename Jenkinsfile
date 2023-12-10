pipeline {
    agent any
    environment {
        SCANNER_HOME=tool "sonar-scanner"
    }
    stages {
        stage ('git checkout') {
            steps {
                script {
                    git branch: 'main', credentialsId: 'github-cred', url: 'https://github.com/selvasathis/microservices-shopping.git'
                }
            }
        }
        stage ('sonar scan') {
            steps {
                sh """$SCANNER_HOME/bin/sonar-scanner -Dsonar.projectKey=10-tier -Dsonar.projectName=10-tier -Dsonar.java.bineries= . """
            }
        }
    }
}