pipeline {
    agent any

    environment {
        CI = 'true'
    }

    stages {

        stage('Build') {
            steps {
                sh 'npm install'
            }
        }

        stage('Test') {
            steps {
                sh 'npm run test'
            }
        }

        stage('Containerize') {
            steps {
                sh 'docker build -t tommyzizii/todo-app:latest .'
            }
        }

        stage('Push') {
            steps {
                echo 'Pushing Docker image...'
                sh 'docker push tommyzizii/todo-app:latest'
            }
        }

        stage('Deploy') {
            steps {
                echo 'Deploying...'
            }
        }
    }
}