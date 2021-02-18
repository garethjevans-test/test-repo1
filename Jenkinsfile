pipeline {
  agent any

  options {
    buildDiscarder(logRotator(numToKeepStr: '10'))
    timeout(time: 30, unit: 'MINUTES')
    disableConcurrentBuilds()
  }

  stages {
    stage('Init') {
      steps {
        sh 'curl -L -o jx-release-version-linux-amd64.tar.gz https://github.com/jenkins-x-plugins/jx-release-version/releases/download/v2.2.3/jx-release-version-linux-amd64.tar.gz'
        sh 'tar xvfz jx-release-version-linux-amd64.tar.gz'
        sh 'jx-release-version'
      }
    }
    stage('Stage One') {
      steps {
        sh 'echo "Do Nothing...this is a fork"'  
      }
    }
    stage('Stage Two') {
      steps {
        sh 'echo "Do Nothing...this is a fork"'
      }
    }
    stage('Stage Three') {
      steps {
        sh 'echo "Do Nothing...this is a fork"'
      }
    }
    stage('Stage Four') {
      steps {
        sh 'echo "Do Nothing...XXX"'
      }
    }
  }
}
