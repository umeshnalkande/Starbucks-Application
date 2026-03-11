pipeline {
    agent any
    tools {
        jdk 'jdk17'
        nodejs 'nodejs16'
    }
    stages {
        stage ("Clean Workspace") {
            steps {
                cleanWs()
            }
        }
        stage ("Git Checkout") {
            steps {
                git branch: 'main', url: 'https://github.com/CloudDevOpsHub/Starbucks-Application.git'
            }
        }
        stage("Install NPM Dependencies") {
            steps {
                sh "npm install"
            }
        }
        stage("Build Docker Image") {
            steps {
                sh "docker build -t starbucks ."
            }
        }
        stage("Tag & Push to DockerHub") {
            steps {
                script {
                    withDockerRegistry(credentialsId: 'docker') {
                        sh "docker tag starbucks umeshnalkande/starbucks:latest"
                        sh "docker push umeshnalkande/starbucks:latest"
                    }
                }
            }
        }
    }
}
