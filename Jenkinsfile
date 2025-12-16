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

        stage('Locate pom.xml') {
            steps {
                script {
                    def poms = sh(
                        script: "find . -name pom.xml",
                        returnStdout: true
                    ).trim().split("\n")

                    if (poms.size() == 0) {
                        error "No pom.xml found in repository"
                    }

                    if (poms.size() > 1) {
                        error "Multiple pom.xml files found: ${poms}"
                    }

                    env.POM_PATH = poms[0]
                    echo "Using POM: ${env.POM_PATH}"
                }
            }
        }

        stage('Build') {
            steps {
                sh 'mvn -f ${POM_PATH} clean install'
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
