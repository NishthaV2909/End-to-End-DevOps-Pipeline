pipeline {
    agent any

    stages {

        stage('Build Docker Image') {
            steps {
                bat 'docker build -t devops-demo:latest .'
            }
        }

        stage('Stop Old Container') {
            steps {
                bat 'docker stop devops-demo-container || exit 0'
                bat 'docker rm devops-demo-container || exit 0'
            }
        }

        stage('Run Docker Container') {
            steps {
                bat 'docker run -d -p 5000:5000 --name devops-demo-container devops-demo:latest'
            }
        }

        stage('Test Application') {
            steps {
        bat '''
        echo Waiting for application to start...

        powershell -Command "Start-Sleep -Seconds 3"

        echo Testing application...

        curl --fail --retry 5 --retry-delay 2 http://localhost:5000

        echo.
        echo Application test successful!
            }
        }
    }
}