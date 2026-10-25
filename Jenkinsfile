
pipeline {
    agent any

    stages {
        stage('Build Docker Image') {
            steps {
                bat 'docker build -t week8-registration:v1 .'
            }
        }

        stage('Run Application') {
            steps {
                bat 'docker rm -f week8-registration-ci || exit /b 0'
                bat 'docker run -d --name week8-registration-ci -p 5001:5000 week8-registration:v1'
            }
        }

        stage('Verify Container') {
            steps {
                bat 'docker ps'
                bat 'docker logs week8-registration-ci'
            }
        }
    }

    post {
        success {
            echo 'Week 8 pipeline completed successfully!'
        }
        failure {
            echo 'Pipeline failed. Check the console output.'
        }
    }
}
