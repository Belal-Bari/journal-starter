pipeline {
    agent any

    stages {
        stage('Run Tests in Agent') {
            agent {
                docker {
                    image "docker-agent"
                    args '-v /var/run/docker.sock:/var/run/docker.sock -v $WORKSPACE:/workspace -w /workspace --user root'
                    
                }
            }
            steps {
                echo 'Inside docker-agent'
                sh '''
                    docker --version
                    docker-compose --version
                    docker compose up -d
                    echo "Waiting for services..."
                    sleep 10
                    echo "Waiting for Postgres to be ready..."
                    until docker compose exec postgres pg_isready -U postgres; do
                        sleep 2
                    done
                    echo 'Creating table entries'
                    docker compose exec postgres psql -U postgres -d journal_db -c '
                    CREATE EXTENSION IF NOT EXISTS \"uuid-ossp\";
                    CREATE TABLE IF NOT EXISTS entries (
                        id UUID PRIMARY KEY DEFAULT uuid_generate_v4(),
                        data JSON NOT NULL,
                        created_at TIMESTAMPTZ NOT NULL DEFAULT NOW(),
                        updated_at TIMESTAMPTZ NOT NULL DEFAULT NOW()
                    );'
                    echo "Checking tables in journal_db..."
                    docker compose exec postgres psql -U postgres -d journal_db -c "\\dt"
                    docker compose exec backend_api curl -X POST http://localhost:8000/entries \
                    -H "Content-Type: application/json" \
                    -d '{
                        "work": "Learned FastAPI basics",
                        "struggle": "Understanding async/await",
                        "intention": "Practice more with FastAPI"
                    }'
                    docker compose exec backend_api curl http://localhost:8000/entries
                    docker compose logs backend_api
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
