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
                    def processes = sh(script: "lsof -ti:${port}", returnStdout: true).trim()
                    if (processes) {
                        sh "kill -9 ${processes}"
                    } else {
                        echo "No process found on port ${port}"
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
