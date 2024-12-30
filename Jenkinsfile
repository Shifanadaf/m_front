pipeline {
    agent any
    tools {
        nodejs 'sonarnode' // Name of the Node.js installation in Jenkins
    }

    environment {
        NODEJS_HOME = 'C:\\Program Files\\nodejs'  // Set the Node.js path
        SONAR_SCANNER_PATH = 'D:\\sonar-scanner-6.2.1.4610-windows-x64\\bin'
    }

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Install Dependencies') {
            steps {
                bat '''
                set PATH=%NODEJS_HOME%;%PATH%
                npm install
                '''
            }
        }

        

        stage('Build') {
            steps {
                bat '''
                set PATH=%NODEJS_HOME%;%PATH%
                cd frontend/register
                npm run build
                '''
            }
        }

       
        stage('SonarAnalysis'){
            environment{
                SONAR_TOKEN=credentials('sonarqube-token')
            }
             steps{
                bat '''
                sonar-scanner ^
                -Dsonar.projectKey=mernfront ^
                -Dsonar.sources=. ^
                -Dsonar.host.url=http://localhost:9000 ^
                -Dsonar.token=sqp_8a68cf1ae047e76c978fe5e6260e414b06df2c99 ^
                '''
            }
       
        }}

    post {
        success {
            echo 'Pipeline completed successfully'
        }
        failure {
            echo 'Pipeline failed'
        }
        always {
            echo 'This runs regardless of the result.'
        }
    }
}

