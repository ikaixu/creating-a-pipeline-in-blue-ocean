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
        sh 'npm config set registry http://registry.npm.taobao.org'
        sh 'npm config get registry'
        sh 'npm install -g cnpm --registry=https://registry.npm.taobao.org'
        sh 'cnpm -v'
        sh 'cnpm install'
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