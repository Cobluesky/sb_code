pipeline {
  agent any
  // any, none, label, node, docker, dockerfile, kubernetes
  tools {
    maven 'my_maven'
  }
  environment {
    gitName = 'Cobluesky'
    gitEmail = 'habuhamo900@gmail.com'
  }
  stages {
    stage('Example') {
      steps {
        echo 'Hello World'
        }
    }
  }
}
