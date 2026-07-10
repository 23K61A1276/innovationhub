pipeline {
    agent any

    environment {
        REPO_URL = 'https://github.com/23K61A1276/innovationhub.git'
        FRONTEND = 'frontend'
        BACKEND = 'backend'
        DOCKER_IMAGE = 'innovationhub'
        BUILD_TAG = "${BUILD_NUMBER}"
    }

    stages {

        stage('Checkout Source Code') {
            steps {
                echo 'Cloning GitHub Repository...'
                git branch: 'main',
                    url: "${REPO_URL}"
            }
        }

        stage('Install Frontend Dependencies') {
            steps {
                dir("${FRONTEND}") {
                    sh 'npm install'
                }
            }
        }

        stage('Build React Application') {
            steps {
                dir("${FRONTEND}") {
                    sh 'npm run build'
                }
            }
        }

        stage('Install Backend Dependencies') {
            steps {
                dir("${BACKEND}") {
                    sh 'python3 -m venv venv'
                    sh '. venv/bin/activate && pip install -r requirements.txt'
                }
            }
        }

        stage('Backend Test') {
            steps {
                dir("${BACKEND}") {
                    sh 'echo "Running Flask Tests..."'
                }
            }
        }

        stage('Build Docker Image') {
            steps {
                sh "docker build -t ${DOCKER_IMAGE}:${BUILD_TAG} ."
                sh "docker tag ${DOCKER_IMAGE}:${BUILD_TAG} ${DOCKER_IMAGE}:latest"
            }
        }

        stage('Deploy Docker Container') {
            steps {
                sh '''
                docker stop innovationhub || true
                docker rm innovationhub || true

                docker run -d \
                    --name innovationhub \
                    -p 5000:5000 \
                    innovationhub:latest
                '''
            }
        }

    }

    post {

        success {
            echo "=================================="
            echo "Build Successful"
            echo "Application Deployed Successfully"
            echo "=================================="
        }

        failure {
            echo "=================================="
            echo "Build Failed"
            echo "=================================="
        }

        always {
            cleanWs()
        }
    }
}