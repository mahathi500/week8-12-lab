
pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Build Docker Image') {
            steps {
                bat 'docker build -t mahathinalagandla/week8-registration:v1 .'
            }
        }

        stage('Push Docker Image') {
            steps {
                bat 'docker push mahathinalagandla/week8-registration:v1'
            }
        }

        stage('Deploy to Kubernetes') {
            steps {
                bat 'kubectl apply -f k8s/deployment.yaml'
                bat 'kubectl apply -f k8s/service.yaml'
            }
        }

        stage('Verify Deployment') {
            steps {
                bat 'kubectl rollout status deployment/week8-registration --timeout=90s'
                bat 'kubectl get pods'
                bat 'kubectl get services'
            }
        }
    }

    post {
        success {
            echo 'Week 9 Jenkins-Kubernetes pipeline completed!'
        }
        failure {
            echo 'Pipeline failed. Check Console Output.'
        }
    }
}
