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
                        def processes = sh(script: "lsof -ti:${port}", returnStdout: true).trim()
                        if (processes) {
                            sh "kill ${processes}"
                            echo "Terminated processes on port ${port}"
                        } else {
                            echo "No process found on port ${port}"
                        }
                    } catch (Exception e) {
                        echo "Error checking port availability: ${e.message}"
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
