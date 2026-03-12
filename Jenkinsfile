pipeline {

    agent any

    stages {

        stage('Build') {
            agent {
                docker {
                    image 'node:18'
                    args '-u root'
                }
            }
            steps {
                sh '''
                apt-get update
                apt-get install -y python3 python-is-python3 build-essential
                PUPPETEER_SKIP_DOWNLOAD=true npm install
                '''
            }
        }

        stage('Test') {
            agent {
                docker {
                    image 'node:18'
                    args '-u root'
                }
            }
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
        echo 'Logging into Docker Hub and pushing image...'

        withCredentials([usernamePassword(
            credentialsId: "${DOCKER_HUB_CREDS}",
            usernameVariable: 'DOCKER_USER',
            passwordVariable: 'DOCKER_PASS'
        )]) {

            sh "echo $DOCKER_PASS | docker login -u $DOCKER_USER --password-stdin"

            sh "docker push ${DOCKER_HUB_USER}/${IMAGE_NAME}:latest"
        }
    }
}

        stage('Deploy') {
            steps {
                echo "Deploying..."
            }
        }

    }
}