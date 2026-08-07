pipeline {
    agent any

    tools {
        nodejs 'NodeJS20'
    }

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/keshavmallawat/team_eta.git'
            }
        }

        stage('Install Dependencies') {
            steps {
                bat 'npm install'
            }
        }

        stage('Lint') {
            steps {
                bat 'npm run lint'
            }
        }

        stage('Build') {
            steps {
                bat 'npm run build'
            }
        }
    }

    post {
        success {
            echo 'Build completed successfully!'
            archiveArtifacts artifacts: '.next/**', fingerprint: true, allowEmptyArchive: true
        }
        failure {
            echo 'Build failed.'
        }
    }
}
