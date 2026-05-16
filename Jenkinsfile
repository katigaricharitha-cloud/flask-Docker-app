pipeline {
    agent any

    stages {

        stage("Checkout") {
            steps {
                checkout scm
            }
        }

        stage("Check Files") {
            steps {
                bat 'dir'
            }
        }

        stage("Build Docker Image") {
            steps {
                bat 'docker build -t flask-sqlite-app .'
            }
        }

        stage("Stop Old Container") {
            steps {
                bat 'docker stop flask-container || exit 0'
                bat 'docker rm flask-container || exit 0'
            }
        }

        stage("Run Container") {
            steps {
                bat 'docker run -d -p 8083:5001 --name flask-container flask-sqlite-app'
            }
        }
    }
}
