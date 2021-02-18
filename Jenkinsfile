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
        sh './jx-release-version'
      }
    }
    stage('Change Request') {
      when ( changeRequest() )
      steps {
        echo "Change Request"  
      }
    }
    stage('Tag') {
      when ( buildingTag() )
      steps {
        echo "Tag"
      }
    }
    stage('Release') {
      when ( branch 'main' )
      steps {
        echo "Release"
      }
    }
  }
}
