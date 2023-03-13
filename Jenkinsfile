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
        sh 'docker build -t anthonymikha/capstone-project .'
      }
    }

    stage('run') {
      steps {
        sh 'docker run --name app -p 80:80 -d anthonymikha/capstone-project'
      }
    }

    stage('test') {
      steps {
        sh 'curl aws-machine-IP:80 '
      }
    }

    stage('Login') {
      steps {
        sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'
      }
    }

    stage('Push') {
      steps {
        sh 'docker push anthonymikha/capstone-project'
      }
    }
    // stage('logout') {
    //  steps {
    //   sh 'docker logout'
    //	 sh 'docker stop app'
    //	 sh 'docker rm app'
    // }
    }
  }
 }
