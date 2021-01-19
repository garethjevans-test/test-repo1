pipeline {
  agent any

  options {
    buildDiscarder(logRotator(numToKeepStr: '10'))
    timeout(time: 30, unit: 'MINUTES')
    disableConcurrentBuilds()
  }

  stages {
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
