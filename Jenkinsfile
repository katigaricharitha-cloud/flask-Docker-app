pipeline {
    agent any

    stages {

        stage("Checkout") {
            steps {
                echo "===== Checking out code ====="
                checkout scm
            }
        }

        stage("Clean Workspace") {
            steps {
                echo "===== Cleaning workspace ====="
                cleanWs()
            }
        }

        stage("Build Docker Image") {
            steps {
                echo "===== Building Docker image ====="
                bat 'docker build -t userresource-app:latest .'
            }
        }

        stage("Stop Old Container") {
            steps {
                echo "===== Stopping old container ====="
                bat 'docker stop user-container || exit 0'
                bat 'docker rm user-container || exit 0'
            }
        }

        stage("Run Container") {
            steps {
                echo "===== Running new container ====="
                bat 'docker run -d -p 8081:5000 --name user-container userresource-app:latest'
            }
        }
    }

    post {
        success {
            echo "===== DEPLOYMENT SUCCESS ====="
        }

        failure {
            echo "===== BUILD FAILED ====="
        }
    }
}
