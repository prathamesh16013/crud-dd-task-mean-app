pipeline {
    agent any

    environment {
        GIT_CREDENTIALS = 'github-creds'              // GitHub credentials ID
        DOCKER_HUB_CREDENTIALS = 'dockerhub-id'       // Docker Hub credentials ID
        
        FRONTEND_IMAGE = 'pratham16013/mean-app-fe'
        BACKEND_IMAGE  = 'pratham16013/mean-app-be'
        IMAGE_TAG = "latest"

        DEPLOY_DIR = '/home/ubuntu/mean-docker'
    }

    stages {

        stage('Checkout Code') {
            steps {
                git branch: 'master',
                    credentialsId: "${GIT_CREDENTIALS}",
                    url: 'https://github.com/prathamesh16013/crud-dd-task-mean-app.git'
            }
        }

        stage('Build Backend Image') {
            steps {
                script {
                    docker.build("${BACKEND_IMAGE}:${IMAGE_TAG}", './backend')
                }
            }
        }

        stage('Build Frontend Image') {
            steps {
                script {
                    docker.build("${FRONTEND_IMAGE}:${IMAGE_TAG}", './frontend')
                }
            }
        }

        stage('Push Images to Docker Hub') {
            steps {
                withCredentials([usernamePassword(
                    credentialsId: "${DOCKER_HUB_CREDENTIALS}",
                    usernameVariable: 'DOCKER_USER',
                    passwordVariable: 'DOCKER_PASS'
                )]) {
                    sh """
                        echo "$DOCKER_PASS" | docker login -u "$DOCKER_USER" --password-stdin
                        docker push ${BACKEND_IMAGE}:${IMAGE_TAG}
                        docker push ${FRONTEND_IMAGE}:${IMAGE_TAG}
                    """
                }
            }
        }

        stage('Deploy to EC2 via Docker Compose') {
            steps {
                dir("${DEPLOY_DIR}") {
                    sh """
                        docker-compose down
                        docker-compose pull
                        docker-compose up -d --build
                    """
                }
            }
        }
    }
}
