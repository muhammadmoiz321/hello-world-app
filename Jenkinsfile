pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                bat 'npm install'
            }
        }
        stage('SonarQube Scan') {
            environment {
                scannerHome = tool 'sonar-scanner'
            }
            steps {
                // Execute SonarQube Scanner
                withSonarQubeEnv('server-sonar') {
                        bat "${scannerHome}/bin/sonar-scanner.bat -Dsonar.projectKey=Hello_world_app -Dsonar.sources=. -Dsonar.host.url=http://localhost:9000"
                }
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
