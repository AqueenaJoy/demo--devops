pipeline {
    agent any

    environment {
        IMAGE_NAME = "flask-app"
        CONTAINER_NAME = "flask"
        PORT = "5000"
    }

    stages {

        stage('Checkout Code') {
            steps {
                git branch: 'main', url: 'https://github.com/AqueenaJoy/demo--devops.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                bat "docker build -t %IMAGE_NAME% ."
            }
        }

        stage('Stop & Remove Old Container') {
            steps {
                bat '''
                REM Stop the container if it exists
                docker ps -q -f "name=%CONTAINER_NAME%" > nul 2>&1 && docker stop %CONTAINER_NAME% || echo "No running container to stop"
                
                REM Remove the container if it exists
                docker ps -aq -f "name=%CONTAINER_NAME%" > nul 2>&1 && docker rm %CONTAINER_NAME% || echo "No container to remove"
                '''
            }
        }

        stage('Run Container') {
            steps {
                bat "docker run -d -p %PORT%:%PORT% --name %CONTAINER_NAME% %IMAGE_NAME%"
            }
        }
    }

    post {
        success {
            echo "Pipeline completed successfully!"
        }
        failure {
            echo "Pipeline failed. Check logs."
        }
    }
}
