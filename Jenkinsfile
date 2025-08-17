pipeline {
    agent any

    stages {
        stage('Build') {
            agent {
                docker {
                    image 'docker:20.10-dind'
                    args '--privileged -v /var/lib/docker'
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