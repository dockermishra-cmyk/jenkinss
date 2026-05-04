pipeline {
    agent any

    environment {
        // Set the NodeJS version if needed, e.g., 'nodejs-lts'
        NODE_HOME = tool name: 'NodeJS', type: 'NodeJSInstallation'
    }

    stages {
        stage('Checkout') {
            steps {
                // Checkout the code from the GitHub repository
                git 'https://github.com/yourusername/your-repository-name.git'
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

        stage('Install Dependencies') {
            steps {
                script {
                    // Install Node.js dependencies
                    sh 'npm install'
                }
            }
        }

        stage('Run Tests') {
            steps {
                script {
                    // Run your tests, if any (e.g., `npm test`)
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