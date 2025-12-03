pipeline {
    agent any

    environment {
        git_branch = 'master'
        git_url    = 'https://github.com/Neeraj999999/Amazon-ABC.git'
    }

    tools {
        maven 'MavenLocal'
        jdk   'JDK21'
    }

    stages {

        stage('clone project') {
            steps {
                git branch: "${git_branch}", url: "${git_url}"
            }
        }

        stage('clean') {
            steps {
                dir('Amazon') {
                    sh 'mvn clean'
                }
            }
        }

        stage('compile') {
            steps {
                dir('Amazon') {
                    sh 'mvn compile'
                }
            }
        }

        stage('test') {
            steps {
                dir('Amazon') {
                    sh 'mvn test'
                }
            }
        }

        stage('build') {
            steps {
                dir('Amazon') {
                    sh 'mvn clean install'
                }
            }
        }
    }

    post {
        always {
            echo 'Post: ALWAYS executed.'
        }
        success {
            echo 'Post: Build SUCCESS.'
        }
        failure {
            echo 'Post: Build FAILURE.'
        }
        unstable {
            echo 'Post: Build UNSTABLE.'
        }
        aborted {
            echo 'Post: Build ABORTED.'
        }
    }
}
