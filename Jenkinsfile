
pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                echo 'Starting SheShield pipeline'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build --no-cache -t sheshield:1.0 .'
            }
        }

        stage('Stop Old Container') {
            steps {
                sh 'docker rm -f sheshield-container || true'
            }
        }

        stage('Deploy Container') {
            steps {
                sh 'docker run -d --name sheshield-container -p 8082:80 sheshield:1.0'
            }
        }

        stage('Verify Deployment') {
            steps {
                sh 'docker ps'
            }
        }
    }

    post {
        success {
            echo 'SheShield deployed successfully!'
        }
        failure {
            echo 'SheShield deployment failed!'
        }
    }
}
