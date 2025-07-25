pipeline {
    agent any

    tools {
        maven 'Maven3'    // Make sure you configure Maven in Jenkins Global Tools
        jdk 'JDK17'       // Make sure JDK 17 is configured too
    }

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Build with Maven') {
            steps {
                sh 'mvn clean package -DskipTests'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t demo-app:latest .'
            }
        }

        stage('Run Docker Container') {
            steps {
                sh 'docker run -d -p 8080:8080 --name demo-app demo-app:latest'
            }
        }
    }
    post {
        always {
            sh 'docker stop demo-app || true'
            sh 'docker rm demo-app || true'
        }
    }
}
