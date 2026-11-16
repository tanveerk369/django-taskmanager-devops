
pipeline {
    agent any

    stages {

        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Django Validation') {
            steps {
                sh '''
                    docker compose up -d db
                    docker compose run --rm web python manage.py check
                '''
            }
        }
    }

    post {
        success {
            echo 'Initial CI pipeline completed successfully!'
        }

        failure {
            echo 'Pipeline failed. Check the console output.'
        }
    }
}
