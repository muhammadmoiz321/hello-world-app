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
                sh 'docker build -t helloworld .'
                sh 'docker run -d -p 3000:3000 helloworld'
            }
        }
    }
}

