pipeline {
    agent any

    stages {
        stage('Build') {
            agent {
                docker {
                    image 'docker:24-cli'
                    args '-v /var/run/docker.sock:/var/run/docker.sock'
                    reuseNode true
                }
            }
            steps {
                echo 'Building...'
                sh '''
                    docker version
                    docker build -t test_app:ver1.0 .
                    docker ps
                    docker images | grep test_app
                '''

            }
        }
    }
}