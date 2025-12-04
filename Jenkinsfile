pipeline {
    agent any

    tools {
        maven 'MavenLocal'
        jdk   'JDK21'
    }

    environment {
        git_branch = "${env.BRANCH_NAME}"
    }

    stages {
        stage('Branch Info') {
            steps {
                echo "Building branch: ${env.BRANCH_NAME}"
                echo "Running build on: ${env.NODE_NAME}"
            }
        }

        stage('Checkout Repo') {
            steps {
                git branch: "${env.BRANCH_NAME}", url: 'https://github.com/Neeraj999999/Amazon-ABC.git'
            }
        }

        stage('Build Amazon Project') {
            steps {
                dir('Amazon') {
                    sh 'mvn clean install'
                }
            }
        }
    }

    post {
        success {
            echo "Build SUCCESS for branch: ${env.BRANCH_NAME}"
        }
        failure {
            echo "Build FAILED for branch: ${env.BRANCH_NAME}"
        }
    }
}
