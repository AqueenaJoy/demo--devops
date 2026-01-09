pipeline {
    agent any

    stages {
        stage('Clone Code') {
            steps {
                git branch: 'main',
                    url: 'https://github.com/AqueenaJoy/demo--devops.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                bat 'docker build -t flask-app .'
            }
        }

        stage('Stop Old Container') {
            steps {
                bat '''
                docker stop flask || exit 0
                docker rm flask || exit 0
                '''
            }
        }

        stage('Run Container') {
            steps {
                bat 'docker run -d -p 5000:5000 --name flask flask-app'
            }
        }
    }
}
