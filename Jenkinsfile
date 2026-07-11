pipeline {
    agent any

    environment {
        PYTHON = "python"
        NODE = "npm"
    }

    stages {

        stage('Checkout Source Code') {
            steps {
                git branch: 'main',
                    url: 'https://github.com/23K61A1276/innovationhub.git'
            }
        }

        stage('Install Frontend Dependencies') {
            steps {
                dir('frontend') {
                    bat '%NODE% install'
                }
            }
        }

        stage('Build Frontend') {
            steps {
                dir('frontend') {
                    bat '%NODE% run build'
                }
            }
        }

        stage('Install Backend Dependencies') {
            steps {
                dir('backend') {
                    bat '%PYTHON% -m pip install --upgrade pip'
                    bat '%PYTHON% -m pip install -r requirements.txt'
                }
            }
        }

        stage('Backend Test') {
            steps {
                dir('backend') {
                    bat '%PYTHON% -m pytest'
                }
            }
        }

        stage('Build Successful') {
            steps {
                echo 'Frontend Build Successful'
                echo 'Backend Build Successful'
                echo 'CI Pipeline Completed Successfully'
            }
        }
    }

    post {

        success {
            echo 'SUCCESS: Jenkins Pipeline Completed.'
        }

        failure {
            echo 'FAILED: Please check the console output.'
        }

        always {
            cleanWs()
        }
    }
}
