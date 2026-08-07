pipeline {
        agent any

        tools {
                    nodejs 'NodeJS'
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

                    stage('Build') {
                                    steps {
                                                        echo 'Building the application...'
                                                        bat 'npm run build'
                                    }
                    }

                    stage('Test') {
                                    steps {
                                                        echo 'Running tests / static analysis...'
                                                        bat 'npm run lint'
                                    }
                    }

                    stage('Deploy') {
                                    steps {
                                                        echo 'Deploying application build artifacts...'
                                                        bat 'if not exist deployed mkdir deployed'
                                                        bat 'xcopy /E /I /Y .next deployed\\.next'
                                                        echo 'Deployment completed successfully!'
                                    }
                    }
        }

        post {
                    success {
                                    echo 'Pipeline completed successfully: Build, Test, and Deploy stages passed!'
                                    archiveArtifacts artifacts: '.next/**', fingerprint: true, allowEmptyArchive: true
                    }
                    failure {
                                    echo 'Pipeline failed.'
                    }
        }
}
