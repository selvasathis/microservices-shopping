pipeline {
    agent any
    tools {
        tool name: 'sonar-scanner', type: 'hudson.plugins.sonar.SonarRunnerInstallation'
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
                script {
                    def scannerHome = tool 'sonar-scanner'
                    withSonarQubeEnv ('sonar') {
                        sh '${scannerHome}/bin/sonar-scanner -Dsonar.projectKey=microservice'

                }
                }
            }
        }
    }
}