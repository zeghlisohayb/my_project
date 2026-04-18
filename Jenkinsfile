pipeline {
    agent any

    stages {
        stage('Build Docker Image') {
            steps {
                sh 'docker build -t my-nginx .'
            }
        }

        stage('Run Container') {
            steps {
                sh 'docker run -d -p 8090:80 my-nginx'
            }
        }
    }
}
