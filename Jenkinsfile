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
                script {
                    echo "===== Building Docker Image ====="
                    bat 'docker build -t userresource-app:latest .'
                }
            }
        }

        stage("Stop Old Container") {
            steps {
                script {
                    echo "===== Stopping old container ====="
                    bat 'docker stop userresource-container || exit 0'
                    bat 'docker rm userresource-container || exit 0'
                }
            }
        }

        stage("Run Container") {
            steps {
                script {
                    echo "===== Running new container ====="
                    bat 'docker run -d -p 5000:5000 --name userresource-container userresource-app:latest'
                }
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
