pipeline {
    agent any

    environment {
        CONTAINER_NAME="my-app"
        DATABASE_NAME="MyDatabase"
        DATABASE_PASSWORD="Tu@991227"
        DATABASE_ROOT_PASSWORD="root_password"
        DATABASE_USER="admin"
    }

    stages {
        stage('Checkout') {
            steps {
                git credentialsId: '01d29f67-eb6e-4534-9c77-64aec596380c', url: 'https://github.com/ChangChangLyn/CDCNPM.git', branch: 'main'
            }
        }

        stage('Build and Deploy') {
            steps {
                script {
                    bat 'docker-compose down'
                    bat 'docker-compose up --build'
                }
            }
        }

        stage('Post-deploy Cleanup') {
            steps {
                bat 'docker system prune -f'
            }
        }
    }

    post {
        always {
            archiveArtifacts artifacts: '*/logs/*', allowEmptyArchive: true
        }
    }
}
