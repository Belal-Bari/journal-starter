pipeline {
    agent any

    stages {
        stage('Run Tests in Agent') {
            agent {
                docker {
                    image "docker-agent"
                    args '-v /var/run/docker.sock:/var/run/docker.sock -v $WORKSPACE:/workspace -w /workspace'
                }
            }
            steps {
                echo 'Inside docker-agent'
                sh '''
                    docker --version
                    docker-compose --version
                    docker compose up -d
                    echo "Waiting for services..."
                    sleep 15
                '''
            }
            post {
                always {
                    sh 'docker compose down -v'
                }
            }
        }
    }
}
