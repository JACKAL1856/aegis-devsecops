pipeline {
  agent any

  stages {

    stage('Checkout') {
      steps {
        checkout scm
      }
    }

    stage('Build') {
      steps {
        echo 'Build stage placeholder'
      }
    }

    stage('SAST - Semgrep (Secrets Gate)') {
      steps {
        sh '''
          echo "Running Semgrep SAST secrets scan..."
          export PATH=$PATH:$HOME/.local/bin

          semgrep --version

          # FAIL pipeline on ANY secret finding
          semgrep --config=p/secrets --error .
        '''
      }
    }

    stage('SCA - Dependency Check') {
      steps {
        sh '''
          echo "Running OWASP Dependency-Check SCA scan..."

          # Download Dependency-Check if not present
          if [ ! -d "dependency-check" ]; then
            echo "Downloading OWASP Dependency-Check..."
            curl -sL https://github.com/jeremylong/DependencyCheck/releases/download/v9.0.7/dependency-check-9.0.7-release.zip -o dc.zip
            unzip -q dc.zip
          fi

          # Run scan (FAIL on CVSS >= 7)
          ./dependency-check/bin/dependency-check.sh \
            --project "Aegis DevSecOps" \
            --scan app \
            --format HTML \
            --out dependency-check-report \
            --failOnCVSS 7
        '''
      }
    }
  }

  post {
    success {
      echo 'Pipeline completed successfully'
    }
    failure {
      echo 'Pipeline FAILED due to security gate'
    }
  }
}




