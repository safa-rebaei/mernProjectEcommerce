pipeline {
    agent any
    stages {
        stage('Checkout') {
            steps {
                git credentialsId: 'github-token', url: 'https://github.com/safa-rebaei/mernProjectEcommerce.git'
            }
        }
        stage('Install Backend') {
            steps {
                dir('backend') {
                    sh 'npm install'
                }
            }
        }
        stage('Test Backend') {
            steps {
                dir('backend') {
                    sh 'npm test'
                }
            }
        }
        stage('Build Docker Backend') {
            steps {
                dir('backend') {
                    sh 'docker build -t mern-backend:latest .'
                }
            }
        }
    }
}
