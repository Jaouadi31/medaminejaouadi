pipeline {
    agent any

    environment {
        SONARQUBE = 'http://192.168.33.10:9000'  // SonarQube server URL
        SONAR_TOKEN = 'sqa_b3e5b58a970eee8b48a6df703f097159426f111f'  // Your SonarQube token
    }

    stages {
        // Stage 1: Clone the project from GitHub
        stage('Clone Project') {
            steps {
                git 'https://github.com/Jaouadi31/medaminejaouadi.git'  // Replace with your GitHub repository URL
            }
        }

        // Stage 2: Build the project with Maven
        stage('Build with Maven') {
            steps {
                script {
                    // Compile and build the project using Maven
                    sh 'mvn clean install'
                }
            }
        }

        // Stage 3: Analyze the code with SonarQube
        stage('Analyze with SonarQube') {
            steps {
                script {
                    // Run SonarQube analysis with token for authentication
                    sh 'mvn sonar:sonar -Dsonar.host.url=${SONARQUBE} -Dsonar.login=${SONAR_TOKEN}'
                }
            }
        }

        // Stage 4: Build the Docker image
        stage('Build Docker Image') {
            steps {
                script {
                    // Build the Docker image using the Dockerfile
                    sh 'docker build -t springboot-app .'
                }
            }
        }
    }

    post {
        success {
            echo 'Pipeline completed successfully!'
        }
        failure {
            echo 'Pipeline failed!'
        }
    }
}
