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
                // Build the Docker image
                bat 'docker build -t helloworld .'
                bat 'docker run -d -p 8081:3000 helloworld'
            }
        }
    }
}

