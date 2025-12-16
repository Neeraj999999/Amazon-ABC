pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Build') {
            steps {
                sh "mvn clean install"
            }
        }
    }

    post {
        success {
            echo "Build successful for ${env.JOB_NAME}"
        }
        failure {
            echo "Build failed for ${env.JOB_NAME}"
        }
    }
}
