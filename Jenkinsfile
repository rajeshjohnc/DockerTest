pipeline {
  agent any
  stages {
    stage('Stop Docker') {
      steps {
        sh 'docker stop dockerfile:latest'
      }
    }

    stage('Delete Docker') {
      steps {
        sh 'docker rm dockerfile:latest'
      }
    }

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

    stage('Build') {
      steps {
        sh 'docker build -f Jenkins/Dockerfile -t dockerfile:latest . '
      }
    }

    stage('Docker Run') {
      steps {
        sh 'docker run --name DockerTest -d dockerfile:latest -p 8888:8888'
      }
    }

  }
}