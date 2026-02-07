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
                  echo "Validating presence of DAST report..."
                  echo "Current workspace:"
                  pwd
                  echo "Files in workspace:"
                  ls -l

                  if [ ! -f dast-report.html ]; then
                    echo "DAST report not found!"
                    exit 1
                  fi

                  echo "DAST report found."
                '''
            }
        }

        stage('Publish DAST Report') {
            steps {
                publishHTML(target: [
                    allowMissing: false,
                    alwaysLinkToLastBuild: true,
                    keepAll: true,
                    reportDir: '.',
                    reportFiles: 'dast-report.html',
                    reportName: 'OWASP ZAP DAST Report'
                ])
            }
        }
    }

    post {
        always {
            echo "Archiving DAST report..."
            archiveArtifacts artifacts: 'dast-report.html', fi















