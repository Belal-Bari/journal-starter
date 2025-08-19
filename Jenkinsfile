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
            post {
                always {
                    sh "docker compose down -v"
                }
            }
        }
    }
}
