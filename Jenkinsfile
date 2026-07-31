pipeline {

    agent any

    environment {
        IMAGE_NAME = "flask-app"
        CONTAINER_NAME = "flask-container"
    }

    stages {

        stage('Clean Workspace') {
            steps {
                sh 'rm -rf flaskapp || true'
            }
        }

        stage('Clone Repository') {
            steps {
                sh 'git clone https://github.com/samrajviswasam/flaskapp.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                dir('flaskapp') {
                    sh 'docker build -t $IMAGE_NAME .'
                }
            }
        }

        stage('Remove Old Container') {
            steps {
                sh 'docker rm -f $CONTAINER_NAME || true'
            }
        }

        stage('Run Container') {
            steps {
                sh '''
                    docker run -d \
                    --name $CONTAINER_NAME \
                    -p 5000:5000 \
                    $IMAGE_NAME
                '''
            }
        }
    }

    post {
        success {
            echo "Flask application deployed successfully."
        }
        failure {
            echo "Deployment failed."
        }
    }
}
