pipeline {
    agent any

    environment {
        PROJECT_DIR = "C:/mongodb-crud"
    }

    stages {

        stage('Check Project Files') {
            steps {
                dir("${PROJECT_DIR}") {
                    bat 'dir'
                }
            }
        }

        stage('Stop Old Containers') {
            steps {
                dir("${PROJECT_DIR}") {
                    bat 'docker compose down || exit 0'
                }
            }
        }

        stage('Build Containers') {
            steps {
                dir("${PROJECT_DIR}") {
                    bat 'docker compose build'
                }
            }
        }

        stage('Run Containers') {
            steps {
                dir("${PROJECT_DIR}") {
                    bat 'docker compose up -d'
                }
            }
        }

        stage('Check Running Containers') {
            steps {
                bat 'docker ps'
            }
        }

        stage('Health Check') {
            steps {
                // Wait 15 seconds without using "timeout"
                bat 'ping 127.0.0.1 -n 15 > nul'
               
                // Test app
                bat 'curl http://localhost:3000'
            }
        }
    }

    post {
        success {
            echo 'Deployment Successful!'
        }
        failure {
            echo 'Deployment Failed!'
        }
    }
}