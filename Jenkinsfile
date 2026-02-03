pipeline {
  agent any

  stages {

    stage('Checkout') {
      steps {
        echo 'Checking out source code...'
        checkout scm
      }
    }

    /*
    ============================
    SAST DISABLED FOR PHASE 3
    (Already validated in Phase 2)
    ============================
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

          # Create venv if missing
          if [ ! -d "venv" ]; then
            python3 -m venv venv
          fi

          # Activate venv
          . venv/bin/activate

          # Install dependencies
          pip install --upgrade pip
          pip install -r app/app/requirements.txt

          # Run Flask app
          nohup python app/app/app.py > app.log 2>&1 &

          sleep 10
          echo "Flask app started"
        '''
      }
    }
  }

  post {
    always {
      echo 'Pipeline finished'
    }
  }
}










