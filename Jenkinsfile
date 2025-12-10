pipeline {
    agent any

    environment {
        GIT_CREDENTIALS = 'github-token' // mettre l'ID exact de ton token
    }

    stages {
        stage('Checkout') {
            steps {
                git branch: 'dev', url: 'https://github.com/safa-rebaei/mernProjectEcommerce.git', credentialsId: "${GIT_CREDENTIALS}"
            }
        }

        stage('Install Backend') {
            steps {
                dir('backend') {
                    bat 'npm install'
                }
            }
        }

        stage('Test Backend') {
            steps {
                dir('backend') {
                    bat 'npm test'
                }
            }
        }

        stage('Build Frontend') {
            steps {
                dir('frontend') {
                    bat 'npm install'
                    bat 'npm run build'
                }
            }
        }

        stage('Build Docker Images') {
            steps {
                script {
                    bat 'docker build -t mern-backend:latest ./backend'
                    bat 'docker build -t mern-frontend:latest ./frontend'
                }
            }
        }
    }

    post {
        success {
            echo 'Pipeline exécuté avec succès !'
        }
        failure {
            echo 'Échec du pipeline, vérifier les logs.'
        }
    }
}
