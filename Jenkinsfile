pipeline {
  agent any

  stages {

    stage('Checkout') {
      steps {
        checkout scm
      }
    }

    stage('SAST - Semgrep') {
      steps {
        sh '''
          echo "Running Semgrep SAST..."
          semgrep --config=p/secrets --error .
        '''
      }
    }

    stage('SCA - Dependency Check (Non-Blocking)') {
      steps {
        sh '''
          echo "Running OWASP Dependency-Check (non-blocking)..."

          if [ ! -d "dependency-check" ]; then
            curl -sL https://github.com/jeremylong/DependencyCheck/releases/download/v9.0.7/dependency-check-9.0.7-release.zip -o dc.zip
            unzip -q dc.zip
          fi

          ./dependency-check/bin/dependency-check.sh \
            --project "Aegis DevSecOps" \
            --scan app \
            --format HTML \
            --out dependency-check-report \
            --noupdate || true
        '''
      }
    }

    stage('Run Application') {
      steps {
        sh '''
          echo "Starting Flask app for DAST..."

          cd app

          if [ ! -d "venv" ]; then
            python3 -m venv venv
          fi

          . venv/bin/activate

          pip install --upgrade pip
          pip install -r requirements.txt

          nohup python app.py > app.log 2>&1 &

          sleep 10
        '''
      }
    }
  }

  post {
    always {
      echo "Pipeline finished"
    }
    failure {
      echo "Pipeline failed due to security gate"
    }
  }
}









