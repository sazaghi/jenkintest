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
        stage('Deploy') {
            steps {
                script {
                    echo "Deploying application..."
                    // Gunakan 'bat' jika di Windows, atau 'sh' jika di Linux/MacOS
                    bat '''
                    echo Deploying application...
                    xcopy *.* \\remote-server\path\to\deploy /E /H /C /I
                    '''
                }
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
