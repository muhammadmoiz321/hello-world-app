pipeline {
    agent any

    stages {
    

        stage('Build') {
            steps {
                sh 'npm install'
            }
        }

        stage('Deploy') {
            steps {
                // Modify this line to remove the 'nohup' command
                sh 'docker build -t helloworld .'
                sh 'docker run -d -p 8081:3000 helloworld'
            }
        }
    }
}
