pipeline {
    agent any

    triggers {
        githubPush() // auto-trigger on GitHub webhook push events
    }

    environment {
        IMAGE_NAME = 'ubuntu:latest'
        CONTAINER_NAME = 'jenkins-ubuntu-container'
    }

    stages {
        stage('Pull Docker Image') {
            steps {
                script {
                    echo "Pulling Docker image: ${IMAGE_NAME}"
                    sh "docker pull ${IMAGE_NAME}"
                }
            }
        }

        stage('Run Container') {
            steps {
                script {
                    echo "Running Docker container: ${CONTAINER_NAME}"
                    sh """
                        docker run -dit --name ${CONTAINER_NAME} ${IMAGE_NAME} bash
                    """
                }
            }
        }

        stage('Container Status') {
            steps {
                sh "docker ps -a | grep ${CONTAINER_NAME}"
            }
        }
    }

    post {
        always {
            echo "Cleaning up..."
            sh "docker rm -f ${CONTAINER_NAME} || true"
        }
    }
}