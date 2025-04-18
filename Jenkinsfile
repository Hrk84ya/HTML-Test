pipeline {
    agent {
        docker {
            image 'docker:24.0.6'  // any Docker CLI image
            args '-v /var/run/docker.sock:/var/run/docker.sock'
        }
    }

    stages {
        stage('Check Docker CLI') {
            steps {
                sh 'docker --version'
            }
        }

        stage('Pull Ubuntu Image') {
            steps {
                sh 'docker pull ubuntu:latest'
            }
        }

        stage('Run Container') {
            steps {
                sh 'docker run -dit --name jenkins-ubuntu ubuntu:latest bash'
            }
        }

        stage('List Containers') {
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