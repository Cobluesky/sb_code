pipeline {
  agent any
  // any, none, label, node, docker, dockerfile, kubernetes
  tools {
    maven 'my_maven'
  }
  environment {
    gitName = 'pcmin929'
    gitEmail = 'pcmin929@gmail.com'
    githubCredential = 'git_cre'
  }
  stages {
    stage('Checkout Github') {
      steps {
          checkout([$class: 'GitSCM', branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[credentialsId: githubCredential, url:'https://github.com/Cobluesky/sb_code.git']]])
        }
      post {
        failure {
            echo 'Repository Clone Failure'
        }
        success {
            ehco 'Repository Clone Success'
        }
      }
    }
  }

  stages {
    stage('') {
      steps {
          sh 'mvn clean install'
        }
      post {
        failure {
            echo 'Maven Jar Build Failure'
        }
        success {
            ehco 'Repository Clone Success'
        }
      }
    }
  }
} 
