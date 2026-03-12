pipeline {
    agent {
        docker {
            image 'node:18'
        }
    }

    stages {

        stage('Build') {
            steps {
                sh '''
                apt-get update
                apt-get install -y python3 python-is-python3 build-essential
                PUPPETEER_SKIP_DOWNLOAD=true npm install
                '''
            }
        }

        stage('Test') {
            steps {
                sh 'npm test'
            }
        }

        stage('Containerize') {
            steps {
                sh 'docker build -t todo-app .'
            }
        }

        stage('Push') {
            steps {
                echo "Push image"
            }
        }

        stage('Deploy') {
            steps {
                echo "Deploying..."
            }
        }

    }
}