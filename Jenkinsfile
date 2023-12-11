pipeline {
    agent any
    stages {
        stage ('git checkout') {
            steps {
                script {
                    git branch: 'main', credentialsId: 'github-tocken', url: 'https://github.com/selvasathis/microservices-shopping.git'
                }
            }
        }
    }
}