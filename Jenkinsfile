pipeline {
  agent any
  // any, none, label, node, docker, dockerfile, kubernetes
  tools {
    maven 'my_maven'
  }
  environment {
    gitName = 'Cobluesky'
    gitEmail = 'habuhamo900@gmail.com'
    githubCredential = 'git_cre'
    dockerHubRegistry = 'g1mlet/sbimage'
    dockerHubRegistryCredential = 'docker_cre'
  }
  stages {
    stage('Checkout Github') {
      steps {
          checkout([$class: 'GitSCM', branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[credentialsId: githubCredential, url: 'https://github.com/Cobluesky/sb_code.git']]])
          }
      post {
        failure {
          echo 'Repository clone failure'
        }
        success {
          echo 'Repository clone success'  
        }
      }
    }

    stage('Maven Build') {
      steps {
          sh 'mvn clean install'
          }
      post {
        failure {
          echo 'Maven jar build failure'
        }
        success {
          echo 'Maven jar build success'  
        }
      }
    }
    stage('Docker Image Build') {
      steps {
          sh "docker build -t ${dockerHubRegistry}:${currentBuild.number} ."
          sh "docker build -t ${dockerHubRegistry}:latest ."
          }
      post {
        failure {
          echo 'Docker image build failure'
        }
        success {
          echo 'Docker image build success'  
        }
      }
    }
    stage('Docker Image Push') {
      steps {
          withDockerRegistry(credentialsId: dockerHubRegistryCredential, url: '') {
            sh "docker push -t ${dockerHubRegistry}:${currentBuild.number}"
            sh "docker push -t ${dockerHubRegistry}:latest"
          }
        }
      post {
        failure {
          echo 'Docker image push failure'
          sh "docker rmi ${dockerHubRegistry}:${currentBuild.number}"
          sh "docker rmi ${dockerHubRegistry}:latest"
        }
        success {
          echo 'Docker image push success'
          sh "docker rmi ${dockerHubRegistry}:${currentBuild.number}"
          sh "docker rmi ${dockerHubRegistry}:latest"          
        }
      }
    }
  }
}
