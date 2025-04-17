pipeline {
    agent any

    triggers {
        pollSCM('H/15 * * * *') 
    }

    environment {
        DEPLOY_PORT = '82'
        IMAGE_NAME = 'my-website'
        CONTAINER_NAME = 'my-website-container'
    }

    stages {
        stage('Checkout') {
            steps {
                checkout scm
                script {
                    echo "Branch: ${env.BRANCH_NAME}"
                }
            }
        }

        stage('Build') {
            when {
                anyOf {
                    branch 'main'
                    branch 'develop'
                }
            }
            steps {
                echo "Building the project from ${env.BRANCH_NAME} branch..."
                sh 'echo Building project...'
            }
        }

        stage('Publish') {
            when {
                branch 'main'
            }
            steps {
                echo "Publishing website from main branch on port ${env.DEPLOY_PORT}..."
                sh '''
                    docker build -t ${IMAGE_NAME} .
                    docker rm -f ${CONTAINER_NAME} || true
                    docker run -d -p ${DEPLOY_PORT}:80 --name ${CONTAINER_NAME} ${IMAGE_NAME}
                '''
            }
        }
    }

    post {
        success {
            echo "Pipeline for ${env.BRANCH_NAME} completed successfully."
        }
        failure {
            echo "Pipeline for ${env.BRANCH_NAME} failed."
        }
    }
}