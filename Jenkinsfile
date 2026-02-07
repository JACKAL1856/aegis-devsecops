pipeline {
    agent any

    environment {
        TARGET_URL = "http://host.docker.internal:3000"
    }

    stages {

        stage('Checkout') {
            steps {
                echo 'Checking out source code...'
                checkout scm
            }
        }

        stage('DAST - OWASP ZAP Baseline') {
            steps {
                script {
                    docker.image('zaproxy/zap-stable').inside {
                        sh '''
                        echo "Running OWASP ZAP Baseline Scan..."
                        zap-baseline.py \
                          -t ${TARGET_URL} \
                          -r dast-report.html
                        '''
                    }
                }
            }
        }
    }

    post {
        always {
            echo 'Archiving DAST report...'
            archiveArtifacts artifacts: 'dast-report.html', fingerprint: true
        }
        success {
            echo 'DAST completed successfully'
        }
        failure {
            echo 'DAST failed due to high severity findings'
        }
    }
}













