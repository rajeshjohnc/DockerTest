pipeline {
  agent any
  stages {
    stage('Checkout') {
      steps {
        git(url: 'https://github.com/rajeshjohnc/DockerTest.git', branch: 'main')
      }
    }

    stage('sh') {
      steps {
        sh 'ls -la'
      }
    }

  }
}