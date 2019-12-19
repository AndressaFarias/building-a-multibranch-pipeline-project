# building-a-multibranch-pipeline-project

This repository is for the
[Build a multibranch Pipeline project](https://jenkins.io/doc/tutorials/build-a-multibranch-pipeline-project/)
tutorial in the [Jenkins User Documentation](https://jenkins.io/doc/).

This tutorial uses the same application that the [Build a Node.js and React app
with
npm](https://jenkins.io/doc/tutorials/build-a-node-js-and-react-app-with-npm/)
tutorial is based on. Therefore, you'll be building and testing the same
application but this time, its delivery will be different depending on the Git
branch that Jenkins builds from. That is, the branch being built determines
which delivery stage of your Pipeline is executed.

The `jenkins` directory contains an example of the `Jenkinsfile` (i.e. Pipeline)
you'll be creating yourself during the tutorial and the `scripts` subdirectory
contains shell scripts with commands that are executed when Jenkins processes
either the "Deliver for development" or "Deploy for production" stages of your
Pipeline (depending on the branch that Jenkins builds from).


## Passos Realisados

### Clone do repositório
- Fork o repositório: https://github.com/jenkins-docs/building-a-multibranch-pipeline-project
- Clone do repositório 

### Criação das branches
- Criação de branches _development_ e _production_
    - Será criado apenas um Jenkinsfile (inicialmente no ramo _master_ qu será puxado para os outros ramos), cujos estágios serão executados seletivamente com base no ramo do qual Jenkins está construindo.
    - Dentro do diretório _building-a-multibranch-pipeline-project_ execute os seguintes comandos para criar essas branches (a partir do conteúdo da branch master):
    `git branch development`
    `git branch production`
- Verifique se esses ramos agora existem executando o comando `git branch`

### Criação do projeto Pipeline no Blue Ocean
Ao criar um prjeto de Pipeline no Blue Ocean, o Que realmente ocorre é que o Jenkins cria um projeto multbranch Pipeline, por trás dos panos. 
- Acesse `http://localhost:8080/blue`
- Clique **New pipeline** para iniciar o assistente de criação do pipeline.
- Escolha o local onde você armazena seu código?, Clique em Git (não no GitHub).
- No campo _Repository URL_ (em Conectar-se a um repositório Git), especifique o caminho do diretório do seu repositório clonado localmente acima
    - For macOS - /home/Documents/GitHub/building-a-multibranch-pipeline-project
    - For Linux - /home/GitHub/building-a-multibranch-pipeline-project
    - For Windows - /home/Documents/GitHub/building-a-multibranch-pipeline-project
 :x: URL do repositório não é reconhecida e credenciais solicitada tb não são reconhecidas

 ### Crie seu Pipeline inicial como um arquivo Jenkins com estágios de construção e teste
O Pipeline será criado como um Jenkinsfile, que será _comitado_ na _branch_ master do repositório Git clonado localmente (building-a-multibranch-pipeline-project)

Primeiro, crie um Pipeline inicial para baixar uma imagem do Node Docker e execute-a como um contêiner do Docker que criará seu aplicativo Node.js. e React simple. Adicione também um estágio "Build" ao Pipeline para começar a orquestrar todo o processo e um stage "Test" para verificar se o aplicativo é renderizado satisfatoriamente.

~~~groovy
pipeline {
    agent {
        docker {
            image 'node:6-alpine'
            args '-p 3000:3000 -p 5000:5000' 
        }
    }
    environment {
        CI = 'true'
    }
    stages {
        stage('Build') {
            steps {
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
~~~

- Salve o Jenkinsfile editado e o comite no repositório Git local de construção do projeto `building-multibranch-pipeline-project`. Por exemplo. No diretório building-a-multibranch-pipeline-project, execute os comandos:
`


