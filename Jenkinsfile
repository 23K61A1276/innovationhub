pipeline {
    agent any

    stages {

        stage('Checkout') {
            steps {
                git branch: 'main',
                    url: 'https://github.com/23K61A1276/innovationhub.git'
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
                    bat 'py -m pip install --upgrade pip'
                    bat 'py -m pip install -r requirements.txt'
                }
            }
        }

        stage('Backend Test') {
            steps {
                dir('backend') {
                    bat '''
                    if exist app.py (
                        echo Backend found successfully.
                    ) else (
                        exit /b 1
                    )
                    '''
                }
            }
        }

        stage('Build Complete') {
            steps {
                echo 'Frontend and Backend Build Successful!'
            }
        }
    }

    post {
        success {
            echo 'Pipeline Completed Successfully.'
        }

        failure {
            echo 'Pipeline Failed.'
        }
    }
}
