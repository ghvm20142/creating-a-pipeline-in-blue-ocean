pipeline {
  agent {
    docker {
      image 'node:6-alpine'
      args '-p 3000:3000'
    }

  }
  stages {
    stage('build') {
      steps {
        sh '''npm config set registry http://registry.npm.taobao.org
npm install'''
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
        sh '''./jenkins/scripts/deliver.sh
./jenkins/scripts/kill.sh'''
        input 'Finished using the web site? (Click "Proceed" to continue)'
      }
    }

  }
}