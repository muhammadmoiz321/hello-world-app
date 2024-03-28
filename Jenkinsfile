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
                bat 'docker build -t helloworld .'
                // Stop the process using port 8081
                bat '''
                    #!/bin/bash
                    PID=$(lsof -t -i:8081)
                    if [ -n "$PID" ]; then
                        echo "Process using port 8081 found with PID $PID. Stopping..."
                        kill -9 $PID
                        echo "Process stopped."
                    else
                        echo "No process found using port 8081."
                    fi
                '''
                // Now run the docker container
                bat 'docker run -d -p 8081:3000 helloworld'
            }
        }
    }
}
