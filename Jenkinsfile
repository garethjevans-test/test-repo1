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
        checkout scm
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
        sh "git config -l"

        //withCredentials([sshUserPrivateKey(credentialsId: '<credential-id>', keyFileVariable: 'SSH_KEY')]) {
        //  sh("git push origin <local-branch>:<remote-branch>")
        //}
        script {
          GIT_CREDS = credentials('github-access-token')
        }
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

        //withCredentials([usernamePassword(credentialsId: 'example-secure', passwordVariable: 'GIT_PASSWORD', usernameVariable: 'GIT_USERNAME')]) {
        //    def encodedPassword = URLEncoder.encode("$GIT_PASSWORD",'UTF-8')
        //    sh "git config user.email admin@example.com"
        //    sh "git config user.name example"
        //    sh "git add ."
        //    sh "git commit -m 'Triggered Build: ${env.BUILD_NUMBER}'"
        //    sh "git push https://${GIT_USERNAME}:${encodedPassword}@github.com/${GIT_USERNAME}/example.git"
        //}
      }
    }
  }
}
