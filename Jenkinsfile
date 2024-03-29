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
                // Define the scannerHome variable using the tool step
                scannerHome = tool name: 'SonarQubeScanner', type: 'hudson.plugins.sonar.SonarRunnerInstallation'
            }
            steps {
                // Execute SonarQube Scanner
                withSonarQubeEnv('server-sonar') {
                    bat "${scannerHome}/bin/sonar-scanner.bat"
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
