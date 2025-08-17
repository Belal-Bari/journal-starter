pipeline {
    agent any

    stages {
        stage('Build') {
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