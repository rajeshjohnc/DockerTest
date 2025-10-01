pipeline {
  agent any
  stages {
    stage('Stop Docker') {
      steps {
        script {
          try {
            echo 'docker stop'
            sh 'docker stop dockertest'

          } catch (Exception e) {

            echo "Stage docker stop failed, but continuing pipeline: ${e.message}"
          }
        }

      }
    }

    stage('Delete Docker') {
      steps {
        script {
          try {
            echo 'docker rm'
            sh 'docker rm dockertest'

          } catch (Exception e) {

            echo "Stage docker rm failed, but continuing pipeline: ${e.message}"
          }
        }

      }
    }

    stage('Delete image') {
      steps {
        script {
          try {
            echo 'docker image delete'
            sh 'docker rmi dockerfile:latest'

          } catch (Exception e) {

            echo "Stage docker rmi failed, but continuing pipeline: ${e.message}"
          }
        }

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
        sh 'docker run --name dockertest -d dockerfile:latest -p 8888:8888 '
      }
    }

  }
}