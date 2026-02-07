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
                    echo "Checking workspace"
                    pwd
                    ls -l

                    if [ ! -f dast-report.html ]; then
                        echo "DAST report not found"
                        exit 1
                    fi

                    echo "DAST report found"
                '''
            }
        }
    }

    post {
        always {
            archiveArtifacts artifacts: 'dast-report.html', fingerprint: true
        }
    }
}















