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
                        // Use 'netstat' to check for processes using a port
                        def processes = sh(script: "netstat -ano | findstr :${port}", returnStdout: true).trim()
                        if (processes) {
                            // Terminate the process using the port
                            sh "taskkill /F /PID ${processes.split()[4]}"
                            echo "Terminated process using port ${port}"
                        } else {
                            echo "No process found using port ${port}"
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
                retry(3) {
                    sh 'docker run -d -p 8081:3000 helloworld'
                }
            }
        }
    }
}
