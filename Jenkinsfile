pipeline {
    agent any

    tools {
        nodejs 'NodeJS' // This name should match the name you provided in Global Tool Configuration
    }

    stages {
        stage('Checkout') {
            steps {
                git 'https://github.com/dockermishra-cmyk/jenkinss'
            }
        }

        stage('Install Dependencies') {
            steps {
                script {
                    // Install Node.js dependencies using npm
                    sh 'npm install'
                }
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    // Build Docker Image using the Dockerfile
                    sh 'docker build -t mongodb-crud .'
                }
            }
        }

        stage('Run Docker Compose') {
            steps {
                script {
                    // Run Docker Compose to start the services
                    sh 'docker-compose up -d'
                }
            }
        }

        stage('Run Tests') {
            steps {
                script {
                    // Run tests if you have them
                    sh 'npm test'
                }
            }
        }

        stage('Clean Up') {
            steps {
                script {
                    // Shut down Docker containers after use
                    sh 'docker-compose down'
                }
            }
        }
    }

    post {
        always {
            // Clean up Docker images and resources if needed
            sh 'docker system prune -f'
        }
    }
}