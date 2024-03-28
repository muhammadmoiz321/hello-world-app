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
                // Modify this line to remove the 'nohup' command
                bat 'docker build -t helloworld .'
                bat 'docker run -d -p 8081:3000 helloworld'
            }
        }
    }
}
