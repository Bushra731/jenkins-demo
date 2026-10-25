pipeline {
    agent any

    environment {
        IMAGE_NAME = 'jenkins-demo'
        CONTAINER_NAME = 'jenkins-demo-app'
    }

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t $IMAGE_NAME:latest .'
            }
        }

        stage('Remove Old Container') {
            steps {
                sh 'docker rm -f $CONTAINER_NAME || true'
            }
        }

        stage('Run Container') {
            steps {
                sh 'docker run -d --name $CONTAINER_NAME -p 3000:3000 $IMAGE_NAME:latest'
            }
        }

        stage('Verify') {
            steps {
                sh 'sleep 5'
                sh 'curl -s http://localhost:3000'
            }
        }
    }

    post {
        success { echo 'Deployment successful!' }
        failure { echo 'Deployment failed!' }
    }
}
