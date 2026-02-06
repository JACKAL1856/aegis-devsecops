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

        /*
        =================================================
        PHASE 2 – SAST (Semgrep)
        (Already validated earlier – kept disabled)
        =================================================
        stage('SAST - Semgrep') {
            steps {
                sh '''
                echo "Running Semgrep SAST secrets scan..."
                semgrep --config=p/secrets --error .
                '''
            }
        }
        */

        stage('SCA - Dependency Check (Non-Blocking)') {
            steps {
                sh '''
                echo "Running OWASP Dependency-Check (non-blocking)..."

                if [ ! -d "dependency-check" ]; then
                  echo "Downloading Dependency-Check..."
                  curl -sL https://github.com/jeremylong/DependencyCheck/releases/download/v9.0.7/dependency-check-9.0.7-release.zip -o dc.zip
                  unzip -q dc.zip
                  mv dependency-check-* dependency-check
                fi

                ./dependency-check/bin/dependency-check.sh \
                  --scan . \
                  --format HTML \
                  --out dependency-check-report || true
                '''
            }
            post {
                always {
                    archiveArtifacts artifacts: 'dependency-check-report/**', fingerprint: true
                }
            }
        }

        stage('Deploy Test App (OWASP Juice Shop)') {
            steps {
                sh '''
                echo "Deploying OWASP Juice Shop for DAST testing..."

                docker rm -f juice-shop || true

                docker run -d \
                  --name juice-shop \
                  -p 3000:3000 \
                  bkimminich/juice-shop
                '''
            }
        }

        stage('DAST - OWASP ZAP Baseline') {
            steps {
                sh '''
                echo "Starting DAST scan with OWASP ZAP (baseline)..."

                docker run --rm \
                  -v $(pwd):/zap/wrk \
                  zaproxy/zap-stable \
                  zap-baseline.py \
                  -t ${TARGET_URL} \
                  -r dast-report.html
                '''
            }
            post {
                always {
                    archiveArtifacts artifacts: 'dast-report.html', fingerprint: true
                }
                failure {
                    echo 'DAST failed due to high severity findings'
                }
            }
        }

    }

    post {
        always {
            echo 'Cleaning up test containers...'
            sh 'docker rm -f juice-shop || true'
        }
        success {
            echo 'Pipeline completed successfully'
        }
        failure {
            echo 'Pipeline failed – check security reports'
        }
    }
}











