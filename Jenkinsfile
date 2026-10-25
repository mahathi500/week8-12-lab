pipeline {
    agent any

    stages {
        stage('Build Docker Image') {
            steps {
                echo "Build Docker Image"
                bat "docker build -t week8-registration:v1 ."
            }
        }

        stage('Docker Login') {
            steps {
                bat 'docker login -u mahathinalagandla -p  Mahathi@123'
            }
        }

        stage('Push Docker Image to Docker Hub') {
            steps {
                echo "Push Docker Image to Docker Hub"
                bat "docker tag week8-registration:v1 mahathinalagandla/week8-registration:v1"
                bat "docker push mahathinalagandla/week8-registration:v1"
            }
        }

        stage('Deploy to Kubernetes') {
            steps {
                bat 'kubectl apply -f k8s/deployment.yaml'
                bat 'kubectl apply -f k8s/service.yaml'
                bat 'kubectl rollout status deployment/week8-registration --timeout=90s'
            }
        }
    }

    post {
        success {
            echo 'Week 9 pipeline completed successfully!'
        }
        failure {
            echo 'Pipeline failed. Please check the logs.'
        }
    }
}
