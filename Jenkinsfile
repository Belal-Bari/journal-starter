pipeline {
    agent {
        docker {
            image 'docker:20.10-dind'
            args '--privileged -v /var/lib/docker'
        }
    }

    stages {
        stage('Build') {
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