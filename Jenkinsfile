pipeline {
    agent any

    stages {
        stage('Build') {
            agent {
                docker {
                    image 'docker-agent:latest'
                    args '-v /var/run/docker.sock:/var/run/docker.sock'
                    reuseNode true
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