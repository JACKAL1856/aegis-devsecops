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

    stage('SAST - Semgrep (Secrets Gate)') {
      steps {
        sh '''
          echo "Running Semgrep SAST secrets scan..."
          export PATH=$PATH:/var/lib/jenkins/.local/bin
          semgrep --version

          # HARD SECURITY GATE — FAIL ON ANY SECRET
          semgrep --config=p/secrets --severity=ERROR --error .
        '''
      }
    }
  }

  post {
    success {
      echo 'Pipeline completed successfully'
    }
    failure {
      echo 'Pipeline FAILED due to SAST security gate'
    }
  }
}


