pipeline {
    agent any

    tools {
        maven 'MavenLocal'
        jdk   'JDK21'
    }

    environment {
        git_branch = "${env.BRANCH_NAME}"
        slackWebhookUrl = "YOUR_WEBHOOK_URL"
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

        stage('Send Slack Notification') {
            steps {
                script {
                    def status = currentBuild.result ?: 'SUCCESS'
                    def message = """
                    {
                        "text": "Pipeline Build Status: ${status}",
                        "attachments": [
                            {
                                "text": "Branch: ${env.BRANCH_NAME} | Node: ${env.NODE_NAME}",
                                "color": "${status == 'SUCCESS' ? 'good' : 'danger'}"
                            }
                        ]
                    }
                    """
                    sh """
                    curl -X POST -H 'Content-type: application/json' --data '${message}' ${slackWebhookUrl}
                    """
                }
            }
        }
    }

    post {
        always {
            script {
                def status = currentBuild.result ?: 'SUCCESS'
                def message = """
                {
                    "text": "Final Build Result: ${status}",
                    "attachments": [
                        {
                            "text": "Branch: ${env.BRANCH_NAME} | Node: ${env.NODE_NAME}",
                            "color": "${status == 'SUCCESS' ? 'good' : 'danger'}"
                        }
                    ]
                }
                """
                sh """
                curl -X POST -H 'Content-type: application/json' --data '${message}' ${slackWebhookUrl}
                """
            }
        }
    }
}
