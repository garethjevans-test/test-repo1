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
      }
    }
    stage('Change Request') {
      when { changeRequest() }
      steps {
        echo "Change Request"
        script {
          version = sh(returnStdout: true, script: './jx-release-version -debug').trim()
        }
        echo "New Version: $version"

        sh "git remote -v"  
      }
    }
    stage('Tag') {
      when { buildingTag() }
      steps {
        echo "Tag"
      }
    }
    stage('Release') {
      when { branch 'main' }
      steps {
        echo "Release"

        script {
          gitCommit = sh(returnStdout: true, script: 'git rev-parse HEAD').trim()
          version = sh(returnStdout: true, script: './jx-release-version').trim()
        }

        echo "Tagging New Version: $version"
        sh "git tag $version"

        echo "Pushing Tag"
        sh "git push origin --tags"
      }
    }
  }
}
