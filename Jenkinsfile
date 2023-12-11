pipeline {
    agent any
    environment {
        SCANNER_HOME = tool 'sonar-scanner'
    }
    stages {
        stage ('git checkout') {
            steps {
                script {
                    git branch: 'main', credentialsId: 'github-tocken', url: 'https://github.com/selvasathis/microservices-shopping.git'
                }
            }
        }
        stage ('sonar-scanner') {
            steps {
                withSonarQubeEnv('sonar') {
                    sh '''$SCANNER_HOME/bin/sonar-scanner \
                    -Dsonar.projectKey=shopping \
                    -Dsonar.projectName=shopping \
                    -Dsonar.sources=src/ \
                    -Dsonar.java.binaries=. '''
                }
            }
        }
        stage ('docker-build') {
            steps {
                parallel (
                    'nexus_login' {
                        script {
                            withCredentials(credentialsId:"nexus-login") {
                                sh 'docker login http://13.233.101.119:8081/repository/my-repo/'
                            }
                        }
                    }
                    'frontend': {
                        dir ('src/frontend/') {
                            sh 'docker build -t 13.233.101.119:8081/frontend:latest'
                            sh 'docker push 13.233.101.119:8081/frontend:latest'
                            sh 'docker rmi -f 13.233.101.119:8081/frontend:latest'

                        }
                    }
                )
            }
        }
    }
}