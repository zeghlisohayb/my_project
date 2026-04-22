pipeline {
    agent any

    stages {
        stage('SonarQube Analysis') {
            steps {
                withCredentials([string(credentialsId: 'sonar-token', variable: 'SONAR_TOKEN')]) {
                    sh '''
                    docker run --rm \
                      -e SONAR_HOST_URL="http://192.168.203.128:9000" \
                      -e SONAR_LOGIN=$SONAR_TOKEN \
                      sonarsource/sonar-scanner-cli \
                      -Dsonar.projectKey=my_project \
                      -Dsonar.sources=.
                    '''
                }
            }
        }

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
