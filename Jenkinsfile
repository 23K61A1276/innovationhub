pipeline {
    agent any

    stages {

        stage('Checkout') {
            steps {
                git branch: 'main',
                    url: 'https://github.com/23K61A1276/innovationhub.git/'
            }
        }

        stage('Install Frontend') {
            steps {
                dir('frontend') {
                    bat 'npm install'
                }
            }
        }

        stage('Build Frontend') {
            steps {
                dir('frontend') {
                    bat 'npm run build'
                }
            }
        }

        stage('Install Backend') {
            steps {
                dir('backend') {
                    bat 'pip install -r requirements.txt'
                }
            }
        }

        stage('Test Backend') {
            steps {
                dir('backend') {
                    bat 'python -m pytest'
                }
            }
        }

        stage('Completed') {
            steps {
                echo 'Build Successful'
            }
        }
    }
}
