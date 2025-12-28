pipeline {
    agent any

    environment {
        DOCKER_HUB_USER  = "lavanyaa12"
        DOCKER_HUB_CREDS = credentials('docker-hub-credentials')
    }

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Docker Build') {
            steps {
                script {
                    sh "docker build -t ${DOCKER_HUB_USER}/backend-app:latest ./Backend"
                    sh "docker build -t ${DOCKER_HUB_USER}/frontend-app:latest ./Frontend"
                }
            }
        }

        stage('Push to Registry') {
            steps {
                script {
                    sh "echo ${DOCKER_HUB_CREDS_PSW} | docker login -u ${DOCKER_HUB_CREDS_USR} --password-stdin"
                    sh "docker push ${DOCKER_HUB_USER}/backend-app:latest"
                    sh "docker push ${DOCKER_HUB_USER}/frontend-app:latest"
                }
            }
        }
    }
    
    post {
        always {
            sh "docker logout"
            cleanWs()
        }
    }
}