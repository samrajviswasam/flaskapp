pipeline {

    agent any

    environment {
        IMAGE_NAME = "flask-app"
    }

    stages {

        stage('Clone Repository') {
            steps {
                sh '''
                git clone https://github.com/samrajviswasam/flaskapp.git
                '''
            }
        }

        stage('Build Docker Image') {
            steps {
                dir('flask-app') {
                    sh 'docker build -t $IMAGE_NAME .'
                }
            }
        }

        stage('Remove Old Container') {
            steps {
                sh 'docker rm -f flask-container || true'
            }
        }

        stage('Run Container') {
            steps {
                sh '''
                docker run -d \
                    --name flask-container \
                    -p 5000:5000 \
                    flask-app
                '''
            }
        }
    }
}
