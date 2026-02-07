pipeline {
    agent any

    stages {

        stage('Checkout') {
            steps {
                echo 'Checking out source code...'
                checkout scm
            }
        }

        stage('DAST Report Validation') {
            steps {
                sh '''
                echo "Validating presence of DAST report..."

                if [ ! -f dast/dast-report.html ]; then
                  echo "DAST report not found!"
                  exit 1
                fi

                echo "DAST report found"
                '''
            }
        }
    }

    post {
        always {
            echo 'Archiving DAST report...'
            archiveArtifacts artifacts: 'dast/dast-report.html', fingerprint: true
        }
        success {
            echo 'Pipeline completed successfully'
        }
        failure {
            echo 'Pipeline failed'
        }
    }
}














