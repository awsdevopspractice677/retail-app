pipeline {
    agent any

    environment {
        AWS_REGION = 'ap-south-1'
        ECR_REPO = '589833671856.dkr.ecr.ap-south-1.amazonaws.com/retail-app'
    }

    stages {

        stage('Checkout') {
            steps {
                echo 'Code checked out from GitHub'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t retail-app:v1 .'
            }
        }

        stage('Login to ECR') {
            steps {
                sh '''
                aws ecr get-login-password --region ap-south-1 | \
                docker login --username AWS --password-stdin \
                589833671856.dkr.ecr.ap-south-1.amazonaws.com
                '''
            }
        }

        stage('Tag Image') {
            steps {
                sh '''
                docker tag retail-app:v1 \
                589833671856.dkr.ecr.ap-south-1.amazonaws.com/retail-app:v1
                '''
            }
        }

        stage('Push Image') {
            steps {
                sh '''
                docker push \
                589833671856.dkr.ecr.ap-south-1.amazonaws.com/retail-app:v1
                '''
            }
        }
    }
}
