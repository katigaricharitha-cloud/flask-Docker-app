pipeline {
    agent any

    stages {

        stage('Checkout Code') {
            steps {
                git branch: 'main', url: 'https://github.com/your-repo.git'
            }
        }

        stage('Clean Workspace') {
            steps {
                cleanWs()
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t sqlite-app .'
            }
        }

        stage('Stop Old Container') {
            steps {
                sh 'docker stop app || true'
                sh 'docker rm app || true'
            }
        }

        stage('Run Container') {
            steps {
                sh 'docker run -d -p 5000:5000 --name app sqlite-app'
            }
        }

    }

    post {
        success {
            echo 'Build and Deployment SUCCESS'
        }

        failure {
            echo 'Build FAILED - check logs'
        }
    }
}
