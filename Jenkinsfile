
pipeline {
    agent any

    stages {

        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Docker Build') {
            steps {
                sh '''
                    docker build -t taskmanagerapp:${BUILD_NUMBER} .
                '''
            }
        }

        stage('Build Verification') {
            steps {
                sh '''
                    docker images taskmanagerapp
                '''
            }
        }

        stage('Deploy Application') {
            steps {
                sh '''
                    docker compose -p taskmanagerapp \
                    -f docker-compose.yml up -d --build
                '''
            }
        }

        stage('Health Check') {
            steps {
                sh '''
                    sleep 10
                    curl -f http://localhost:8000/ || exit 1
                '''
            }
        }
    }

    post {
        success {
            echo 'Application deployed successfully!'
        }

        failure {
            echo 'Pipeline failed. Check the console output.'
        }
    }
}
