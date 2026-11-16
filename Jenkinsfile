
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
    }

    post {
        success {
            echo 'CI pipeline completed successfully!'
        }

        failure {
            echo 'Pipeline failed. Check the console output.'
        }
    }
}
