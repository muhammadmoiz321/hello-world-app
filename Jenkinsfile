pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                bat 'npm install'
            }
        }

        stage('Deploy') {
            steps {
                bat 'docker build -t helloworld .'
                // Stop the process using port 8081
                bat '''
                    @echo off
                    for /f "tokens=5" %%a in ('netstat -aon ^| findstr :8081') do taskkill /F /PID %%a
                '''
                // Now run the docker container
                bat 'docker run -d -p 8081:3000 helloworld'
            }
        }
    }
}
