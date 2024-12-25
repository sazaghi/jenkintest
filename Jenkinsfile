pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/sazaghi/jenkintest.git'
            }
        }
        stage('Install Dependencies') {
            steps {
                bat 'npm install'
                bat 'npm install --save express'
                bat 'npm install --save-dev supertest'
        }
        }
        stage('Run Unit Tests') {
            steps {
                bat 'npm test'
            }
        }
        stage('Run Integration Tests') {
            steps {
                bat 'npm test integration.test.js'
            }
        }
        stage('Deploy'){
            steps {
                sh '''
                echo "Deploying application..."
                scp -r ./* user@server:/path/to/deploy
                ssh user@server "cd /path/to/deploy && npm start"
                '''
            }
        }
    }

    post {
        success {
            echo 'Pipeline finished successfully!'
            mail to: 'your-email@example.com',
                 subject: "Build Success: ${env.JOB_NAME} #${env.BUILD_NUMBER}",
                 body: "The build was successful.\nCheck details: ${env.BUILD_URL}"
        }
        failure {
            echo 'Pipeline failed!'
            mail to: 'your-email@example.com',
                 subject: "Build Failed: ${env.JOB_NAME} #${env.BUILD_NUMBER}",
                 body: "The build failed.\nCheck details: ${env.BUILD_URL}"
        }
    }
}
