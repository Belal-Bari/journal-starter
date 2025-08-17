pipeline {
    agent any

    stages {
        stage('Build') {
            agent {
                docker {
                    image 'docker:24-cli'
                    args '-v /var/run/docker.sock:/var/run/docker.sock'
                }
            }
            steps {
                echo 'Building...'
                sh '''
                    docker build -t test_app:ver1.0 .
                    docker ps
                    docker images
                '''

            }
        }
    }
}