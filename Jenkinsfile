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
        stage('Test') {
            steps {
                echo 'Booting containers: postgres and test_app:latest'
                sh ''' 
                    docker-compose -f compose.yaml up
                    pg_isready -h postgres -p 5432 -U postgres
                    curl -X POST http://localhost:8000/entries \
                    -H "Content-Type: application/json" \
                    -d '{
                        "work": "Learned FastAPI basics",
                        "struggle": "Understanding async/await",
                        "intention": "Practice more with FastAPI"
                    }'
                    curl http://localhost:8000/entries
                '''
            }
        }
    }
}