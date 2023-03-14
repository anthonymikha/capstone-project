pipeline {
  agent any
  options {
    buildDiscarder(logRotator(numToKeepStr: '5'))
  }
  
  environment {
    DOCKERHUB_CREDENTIALS = credentials('dockerhub')
  }

  stages {
    stage('Build') {
      steps {
        sh 'echo ubuntu123 | sudo -S docker build -t anthonymikha/capstone-project .'
      }
    }

    stage('run') {
      steps {
        sh 'sudo docker run --name app -p 80:80 -d miikha/capstone-project'
      }
    }

    stage('test') {
      steps {
        sh 'curl 3.230.0.72:80 '
      }
    }

    stage('Login') {
      steps {
        sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'
      }
    }

    stage('Push') {
      steps {
        sh 'sudo -S ubuntu123 docker push miikha/capstone-project'
      }
    }
    // stage('logout') {
    //  steps {
    //   sh 'sudo -S ubuntu123 docker logout'
    //	 sh 'sudo -S ubuntu123 docker stop app'
    //	 sh 'sudo -S ubuntu123 docker rm app'
    // }
    //}
  }
 }
