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
        sh 'sudo docker build -t anthonymikha/capstone-project .'
      }
    }

    stage('run') {
      steps {
        sh 'sudo docker run --name app -p 80:80 -d anthonymikha/capstone-project'
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
        sh 'sudo docker push anthonymikha/capstone-project'
      }
    }
    // stage('logout') {
    //  steps {
    //   sh 'sudo docker logout'
    //	 sh 'sudo docker stop app'
    //	 sh 'sudo docker rm app'
    // }
    //}
  }
 }
