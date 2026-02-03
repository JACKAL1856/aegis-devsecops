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

    /* =========================
       GATE 1 – SAST (SEMGREP)
       ========================= */
    stage('SAST - Semgrep (Secrets Gate)') {
      steps {
        sh '''
          echo "Running Semgrep SAST secrets scan..."

          export PATH=$PATH:$HOME/.local/bin
          semgrep --version

          # Fail pipeline on ANY secret detection
          semgrep --config=p/secrets --error .
        '''
      }
    }

    /* =========================
       GATE 2 – SCA (DEPENDENCY CHECK)
       ========================= */
    stage('SCA - Dependency Check') {
      steps {
        sh '''
          echo "Running OWASP Dependency-Check SCA scan..."

          if [ ! -d "dependency-check" ]; then
            echo "Downloading OWASP Dependency-Check..."
            curl -sL https://github.com/jeremylong/DependencyCheck/releases/download/v9.0.7/dependency-check-9.0.7-release.zip -o dc.zip
            unzip -q dc.zip
          fi

          ./dependency-check/bin/dependency-check.sh \
            --project "Aegis DevSecOps" \
            --scan app \
            --format HTML \
            --out dependency-check-report \
            --failOnCVSS 7 \
            --noupdate
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





