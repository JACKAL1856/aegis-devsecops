pipeline {
    agent any

    parameters {
        booleanParam(
            name: 'SECURITY_WAIVER',
            defaultValue: false,
            description: 'Approve DAST security waiver to allow pipeline to continue'
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
                    echo "Checking Jenkins workspace..."
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

        stage('DAST Security Gate (CVSS Based)') {
            steps {
                sh '''
                    echo "Evaluating DAST report using CVSS threshold..."

                    if grep -E "CVSS\\s*[7-9]\\.[0-9]" dast-report.html; then
                        echo "CVSS score >= 7.0 detected"

                        if [ "$SECURITY_WAIVER" = "true" ]; then
                            echo "SECURITY WAIVER APPLIED – proceeding despite CVSS threshold"
                        else
                            echo "No waiver provided – failing pipeline due to CVSS policy"
                            exit 1
                        fi
                    else
                        echo "No CVSS >= 7.0 vulnerabilities found – proceeding"
                    fi
                '''
            }
        }

        stage('Secure Secrets Usage') {
            steps {
                withCredentials([
                    string(credentialsId: 'API_TOKEN', variable: 'API_TOKEN')
                ]) {
                    sh '''
                        echo "Running secured step"
                        # Secret is masked automatically by Jenkins
                        # Never echo secrets
                        curl -H "Authorization: Bearer $API_TOKEN" https://example.com || true
                    '''
                }
            }
        }
    }
}













