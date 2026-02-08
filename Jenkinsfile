pipeline {
    agent any

    parameters {
        booleanParam(
            name: 'SECURITY_WAIVER',
            defaultValue: false,
            description: 'Approve pipeline to continue despite High/Critical DAST findings'
        )
    }

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

                  if grep -Ei "(High|Critical)" dast-report.html; then
                    echo "High or Critical vulnerabilities detected"

                    if [ "$SECURITY_WAIVER" = "true" ]; then
                      echo "SECURITY WAIVER APPLIED — proceeding"
                    else
                      echo "No waiver provided — failing pipeline"
                      exit 1
                    fi
                  else
                    echo "No High or Critical vulnerabilities found"
                  fi
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













