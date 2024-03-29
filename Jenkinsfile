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
                //scannerHome = tool name: 'sonar-scanner', type: 'hudson.plugins.sonar.SonarRunnerInstallation'
                scannerHome = tool 'sonar-scanner'
            }
            steps {
                // Execute SonarQube Scanner
                withSonarQubeEnv('server-sonar') {
                    bat "${scannerHome}/bin/sonar-scanner.bat -D"sonar.projectKey=Hello_world_app" -D"sonar.sources=." -D"sonar.host.url=http://localhost:9000" -D"sonar.login=sqp_dac37b7b9ef8d7dd1d61030888cd69ce38bd53fc""
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
