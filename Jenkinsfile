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
          echo "Running Semgrep SAST secrets scan..."
          export PATH=$PATH:$HOME/.local/bin
          semgrep --version
          semgrep --config=p/secrets --error .
        '''
      }
    }

    stage('SCA - Dependency Check') {
      steps {
        sh '''
          echo "Running OWASP Dependency-Check SCA scan (non-blocking)..."

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
            --noupdate || true
        '''
      }
    }

    stage('Run Application') {
      steps {
        sh '''
          echo "Starting Flask application for DAST..."

          if [ ! -d "venv" ]; then
            python3 -m venv venv
          fi

          . venv/bin/activate

          pip install --upgrade pip
          pip install -r app/requirements.txt

          nohup python app/app.py > app.log 2>&1 &
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








