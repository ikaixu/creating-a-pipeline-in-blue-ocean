pipeline {
  agent {
    docker {
      image 'node:6-alpine'
      args '-p 3000:3000'
    }

  }
  stages {
    stage('Build') {
      steps {
        sh 'npm config set unsafe-perm true'
        sh 'npm cache clean --force'
        sh 'npm install --registry=http://registry.npm.taobao.org'
      }
    }
    stage('Test') {
      environment {
        CI = 'true'
      }
      steps {
        sh './jenkins/scripts/test.sh'
      }
    }
    stage('Deliver') {
      steps {
        sh './jenkins/scripts/deliver.sh'
        input 'Finished using the web site?'
        sh './jenkins/scripts/kill.sh'
      }
    }
  }
}