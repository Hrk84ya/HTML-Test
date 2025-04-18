pipeline {
    agent {
        docker {
            image 'docker:20.10.21' // Alpine image with Docker CLI
            args '-v /var/run/docker.sock:/var/run/docker.sock' // Important: mount Docker socket
        }
    }

    stages {
        stage('Pull Docker Image') {
            steps {
                sh 'docker pull ubuntu:latest'
            }
        }
    
    stage('Check Docker') {
            steps {
                sh 'docker --version'
            }
        }

        stage('Run Container') {
            steps {
                sh 'docker run -dit --name jenkins-ubuntu ubuntu:latest bash'
            }
        }

        stage('Container Status') {
            steps {
                sh 'docker ps -a'
            }
        }
    }

    post {
        always {
            sh 'docker rm -f jenkins-ubuntu || true'
        }
    }
}