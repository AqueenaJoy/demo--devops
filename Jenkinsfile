pipeline {
    agent any

    stages {
        stage('Clone Code') {
            steps {
                git 'https://github.com/<aqueenajoy>/demo--devops.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t flask-app .'
            }
        }

        stage('Stop Old Container') {
            steps {
                sh '''
                docker stop flask || true
                docker rm flask || true
                '''
            }
        }

        stage('Run Container') {
            steps {
                sh 'docker run -d -p 5000:5000 fea510724b39'
            }
        }
    }
}
