pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Verify Environment') {
            steps {
                sh '''
                  java --version
                  mvn --version
                '''
            }
        }

        stage('Build All Maven Projects') {
            steps {
                sh '''
                  set -e
                  for pom in $(find . -name pom.xml); do
                    echo "===================================="
                    echo "Building project using $pom"
                    echo "===================================="
                    mvn -f "$pom" clean install
                  done
                '''
            }
        }
    }

    post {
        success {
            echo "All Maven builds completed successfully"
        }
        failure {
            echo "One or more Maven builds failed"
        }
    }
}
