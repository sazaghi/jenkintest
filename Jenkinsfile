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
        stage('Deploy to GitHub') {
            steps {
                bat '''
                git config --global user.email "zaaghisaad@gmail.com"
                git config --global user.name "sazaghi"
                git add .
                git commit -m "Deploying from Jenkins build #${env.BUILD_NUMBER}"
                git push https://github.com/sazaghi/jenkintest.git main
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
