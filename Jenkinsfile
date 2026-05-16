pipeline {
    agent any

    stages {

        stage("Checkout") {
            steps {
                echo "======== executing checkout ========"
                checkout scm
            }
        }

        stage("Build Docker Image") {
            steps {
                script {
                    echo "======== building docker image ========"
                    bat 'docker build -t userresource-image:latest .'
                }
            }
        }

        stage("Stop Old Container") {
            steps {
                script {
                    echo "======== stopping old container ========"
                    bat 'docker stop userresource-container || exit 0'
                    bat 'docker rm userresource-container || exit 0'
                }
            }
        }

        stage("Deploy Docker Container") {
            steps {
                script {
                    echo "======== running new container ========"
                    bat 'docker run -d -p 5000:5000 --name userresource-container userresource-image:latest'
                }
            }
        }
    }

    post {
        success {
            echo "======== Deployment Successful ========"
        }

        failure {
            echo "======== Deployment Failed ========"
        }
    }
}
