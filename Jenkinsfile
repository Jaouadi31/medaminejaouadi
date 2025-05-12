pipeline {
    agent any

    /*environment {
        SONARQUBE = 'http://192.168.33.10:9000'  // Update the SonarQube server URL if needed
        SONAR_TOKEN = credentials('sonarqube-token')  // This is your secret SonarQube token
    }*/

    stages {
        stage('Entry 0') {
            steps {
                sh 'echo "Entry 1"'  // Replace with your GitHub repository URL
            }
        }
        // Stage 1: Clone the project from GitHub
        stage('Clone Project') {
            steps {
                git branch: 'main',
                url: "https://github.com/Jaouadi31/medaminejaouadi.git"  // Replace with your GitHub repository URL
            }
        }
        stage('Entry 1') {
            steps {
                sh 'echo "Entry 1"'  // Replace with your GitHub repository URL
            }
        }
        // Stage 2: Build the project with Maven
        stage('Build with Maven') {
            steps {
                script {
                    // Compile and build the project using Maven
                    sh 'mvn clean install'
                    sh 'echo "test"'
                }
            }
        }

        // Stage 3: Analyze the code with SonarQube
        stage('Analyze with SonarQube') {
            steps {
                script {
                    sh 'echo "test"'
                    // Run SonarQube analysis with the authentication token
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
