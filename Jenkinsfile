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
          export PATH=$PATH:$HOME/.local/bin

          semgrep --version

          # Secrets-only security gate
          # Any finding = pipeline FAIL
          semgrep --config=p/secrets --error .
        '''
      }
    }

  }

  post {
    success {
      echo 'Pipeline completed successfully'
    }
    failure {
      echo 'Pipeline failed due to security gate'
    }
  }
}

