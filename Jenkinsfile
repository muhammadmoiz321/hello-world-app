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
                    try {
                        sh "lsof -ti:${port}"
                    } catch (Exception e) {
                        echo "Port ${port} is not in use"
                    }
                    echo "Check Port Availability completed"
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
                    def containerId = sh(script: 'docker ps -lq', returnStdout: true).trim()
                    def containerIp = sh(script: "docker inspect -f '{{range .NetworkSettings.Networks}}{{.IPAddress}}{{end}}' $containerId", returnStdout: true).trim()
                    echo "Container IP Address: ${containerIp}"
                }
            }
        }
    }
}
