pipeline {
  agent {
    docker {
      image 'node:6-alpine'
      args '-p 3001:3001 -p 5001:5001'
    }

  }
  stages {
    stage('Build') {
      steps {
        sh 'echo "Hello world!"'
        sh 'npm install'
      }
    }

    stage('Test') {
      steps {
        sh './jenkins/scripts/test.sh'
      }
    }

  }
  environment {
    CI = 'true'
  }
}