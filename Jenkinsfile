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
                    }
                }
            }
        }
        
        stage('Deploy') {
            environment {
                DOCKER_HOST = 'tcp://192.168.1.85:2375' // Replace with the IP address of your Docker host
            }
            steps {
                script {
                    sh 'docker build -t helloworld .'
                    sh 'docker run -d -p 8081:3000 helloworld'
                }
            }
        }
    }
}
