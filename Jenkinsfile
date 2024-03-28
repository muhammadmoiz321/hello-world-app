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
                // Stop the process using port 8081
                bat 'kill $(lsof -t -i:8081)'
                // Now run the Docker container
                bat 'docker run -d -p 8081:3000 helloworld'
            }
        }
    }
}

