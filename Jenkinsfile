pipeline {
    agent any

    stages {

        stage('Checkout') {
            steps {
                git 'https://github.com/katigarcharitha-cloud/flask-Docker-app.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                bat 'docker build -t my-angular-app .'
            }
        }

        stage('Run Container') {
            steps {
                bat 'docker run -d -p 8081:80 my-angular-app'
            }
        }
    }
}
