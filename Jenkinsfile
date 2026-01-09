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
        REM Stop any container using port 5000
        FOR /F "tokens=*" %%i IN ('docker ps -q -f "publish=5000"') DO docker stop %%i
        FOR /F "tokens=*" %%i IN ('docker ps -aq -f "publish=5000"') DO docker rm %%i
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


