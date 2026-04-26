pipeline {
    agent any

    stages {

        stage('Build and Test') {
            stages {

                stage('Install') {
                    steps {
                        bat 'npm install'
                    }
                }

                stage('Test') {
                    steps {
                        bat 'npm run test'
                    }
                }

                stage('Build') {
                    steps {
                        bat 'npm run build'
                    }
                }
            }
        }

        stage('Deployment') {
            when {
                expression { currentBuild.currentResult == 'SUCCESS' }
            }
            stages {

                stage('Deploy to Staging') {
                    when {
                        branch 'development'
                    }
                    steps {
                        echo "🚀 Deploying to STAGING"
                    }
                }

                stage('Deploy to Production') {
                    when {
                        branch 'main'
                    }
                    steps {
                        echo "🔥 Deploying to PRODUCTION"
                    }
                }
            }
        }
    }

    post {
        success {
            echo "✅ TASK COMPLETED"
        }
        failure {
            echo "❌ TASK FAILED"
        }
    }
}
