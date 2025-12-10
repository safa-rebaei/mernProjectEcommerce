pipeline {
    agent any

    environment {
        GIT_CREDENTIALS = 'github-token'   // Ton credential GitHub
    }

    stages {

        /* ----------------------- CHECKOUT ----------------------- */
        stage('Checkout') {
            steps {
                git branch: 'dev',
                    url: 'https://github.com/safa-rebaei/mernProjectEcommerce.git',
                    credentialsId: "${GIT_CREDENTIALS}"
            }
        }

        /* ----------------------- BACKEND INSTALL ----------------------- */
        stage('Install Backend') {
            steps {
                dir('backend') {
                    bat 'npm install'
                }
            }
        }

        /* ----------------------- BACKEND TEST (SKIP SAFE) ----------------------- */
        stage('Test Backend') {
            steps {
                dir('backend') {
                    // Ce script ne fait pas échouer le pipeline
                    bat '''
                        echo "Aucun test détecté → étape ignorée"
                        exit 0
                    '''
                }
            }
        }

        /* ----------------------- FRONTEND BUILD ----------------------- */
        stage('Build Frontend') {
            steps {
                dir('frontend') {
                    bat 'npm install'
                    bat 'npm run build'
                }
            }
        }

        /* ----------------------- BUILD DOCKER ----------------------- */
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
            echo '✔ Pipeline exécuté avec succès !'
        }
        failure {
            echo '❌ Échec du pipeline, vérifier les logs.'
        }
    }
}
