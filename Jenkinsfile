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
            sh 'docker rmi dockerfile:latest -f'

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

    stage('pwd') {
      steps {
        sh 'pwd'
      }
    }

    stage('Build') {
      steps {
        sh 'docker build -f Jenkins/Dockerfile -t dockerfile:latest . '
      }
    }

    stage('Docker Run') {
      steps {
        sh 'docker run --name dockertest --hostname=2d8f71eee95c --user=app --mac-address=f2:e3:49:9a:41:74 --env=PATH=/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin --env=APP_UID=1654 --env=ASPNETCORE_HTTP_PORTS=8080 --env=DOTNET_RUNNING_IN_CONTAINER=true --env=DOTNET_VERSION=9.0.9 --env=ASPNET_VERSION=9.0.9 --env=ASPNETCORE_URLS=http://+:5077 --network=bridge --workdir=/app -p 8081:5077  --runtime=runc -d dockertest:latest'
      }
    }

    stage('Docker Restart') {
      steps {
        sh 'docker update --restart unless-stopped $(docker ps -q)'
      }
    }

  }
}