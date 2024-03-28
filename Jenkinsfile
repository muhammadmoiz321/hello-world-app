pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                sh 'npm install'
            }
        }
        
        stage('Check Port Availability') {
            steps {
                script {
                    def port = 8081
                    def isPortAvailable = sh(script: "sudo netstat -tuln | grep ${port} | wc -l", returnStdout: true).trim() == "0"
                    if (!isPortAvailable) {
                        sh "sudo lsof -ti:${port} | xargs sudo kill"
                    }
                }
            }
        }
        
        stage('Deploy') {
            steps {
                sh 'docker build -t helloworld .'
                sh 'docker run -d -p 8081:3000 helloworld'
            }
        }
    }
}

