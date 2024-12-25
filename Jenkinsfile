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
<<<<<<< HEAD:jenkisnsfile
                bat 'npm install --save-dev supertest'
=======
>>>>>>> 3c33dbd57a40b216411ed9649015586b34a2d0b9:Jenkinsfile
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
    }

    post {
        success {
            echo 'Pipeline finished successfully!'
        }
        failure {
            echo 'Pipeline failed!'
        }
    }
}
