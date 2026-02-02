pipeline {
    agent any

    stages {

        stage('Checkout') {
            steps {
                echo 'Checking out source code'
                checkout scm
            }
        }

        stage('Build') {
            steps {
                echo 'Build stage placeholder'
            }
        }

        stage('SAST - Semgrep') {
            steps {
                sh '''
                  echo "Running Semgrep SAST scan..."
                  export PATH=$PATH:$HOME/.local/bin
                  semgrep --version
                  semgrep --config=auto --severity=ERROR --error .
                '''
            }
        }

    }

    post {
        success {
            echo 'Pipeline completed successfully'
        }
        failure {
            echo 'Pipeline failed due to security gate'
        }
    }
}
