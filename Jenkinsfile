pipeline {
    agent {
        docker { image 'docker-agent' }
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