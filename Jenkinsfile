pipeline {
    //agent any
    agent{
        docker{
            image 'node:6-alpine'
            args '-p 3000:3000 -p 5000:5000' 
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
    }
}

// O significado disso é explicado nos arquivos `jenkins/scripts/deliver-for-deployment.sh` e `jenkins/scripts/deploy-for-production.sh` 
// do seu repositório clonado e são abordados nas seções subseqüentes deste tutorial
