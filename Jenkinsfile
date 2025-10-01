pipeline {
  agent any
  stages {
    stage('Stop Docker') {
          steps {
                script {
                    try {
                        echo 'docker stop'
			                  sh 'docker stop dockerfile:latest'
 
                    } catch (Exception e) {
                       
                        echo "Stage B failed, but continuing pipeline: ${e.message}"
                    }
                }
            }
    }

    stage('Delete Docker') {
          steps {
                script {
                    try {
                        echo 'docker rm'
			                  sh 'docker rm dockerfile:latest'
 
                    } catch (Exception e) {
                       
                        echo "Stage B failed, but continuing pipeline: ${e.message}"
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
        sh 'docker run --name DockerTest -d dockerfile:latest -p 8888:8888'
      }
    }

  }
}