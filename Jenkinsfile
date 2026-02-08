pipeline {
    agent any

    stages {

        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('DAST Report Validation') {
            steps {
                sh '''
                    echo "Checking workspace..."
                    pwd
                    ls -l

                    if [ ! -f dast-report.html ]; then
                        echo "DAST report not found!"
                        exit 1
                    fi

                    echo "DAST report found"
                '''
            }
        }

        stage('DAST Security Gate') {
            steps {
                sh '''
                    echo "Evaluating DAST report for High/Critical vulnerabilities..."

                    if grep -Eiq "(High|Critical)" dast-report.html; then
                        echo "High or Critical vulnerabilities found!"
                        exit 1
                    else
                        echo "No High or Critical vulnerabilities found."
                    fi
                '''
            }
        }
    }

    post {
        always {
            echo "Archiving DAST report..."
            archiveArtifacts artifacts: 'dast-report.html', fingerprint: true
        }

        failure {
            echo "Pipeline failed due to security policy enforcement"
        }

        success {
            echo "Pipeline passed security checks"
        }
    }
}













