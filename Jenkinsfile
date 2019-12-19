pipeline {
    
    agent{

        docker{

            image 'node:6-alpine'
            args '-p 3001:3001 -p 5001:5001' 
            // Este parâmetro args torna o contêiner do Nó (temporariamente) acessível através das portas 3000 e 5000.
        }
    }

    environment {
        CI = 'true'
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

        stage('Deliver for development') {
            when {
                branch 'development'
            }
            steps {
                sh './jenkins/scripts/deliver-for-development.sh'
                input message: 'Finished using the web site? (Click "Proceed" to continue)'
                sh './jenkins/scripts/kill.sh'
            }
        }

        stage('Deploy for production') {
            when {
                branch 'production'
            }
            steps {
                sh './jenkins/scripts/deploy-for-production.sh'
                input message: 'Finished using the web site? (Click "Proceed" to continue)'
                sh './jenkins/scripts/kill.sh'
            }
        }
    }

// O significado disso é explicado nos arquivos `jenkins/scripts/deliver-for-deployment.sh` e `jenkins/scripts/deploy-for-production.sh` 
// do seu repositório clonado e são abordados nas seções subseqüentes deste tutorial

  }