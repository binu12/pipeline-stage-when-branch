pipeline {
  agent any
  stages {
    stage('Build Master') {
      when {
        branch 'master'
      }
      steps {
        echo 'Building master'
      }
    }

    stage('Build Dev') {
          when {
            branch 'dev'
          }
          steps {
            echo 'Building dev'
          }
        }

    stage('tagging') {
      parallel {
        stage('tagging') {
          steps {
            withCredentials(bindings: [usernamePassword(credentialsId: '00d1ed86-e252-4171-97e6-c69de2b7ac90', passwordVariable: 'GIT_PASSWORD', usernameVariable: 'GIT_USERNAME')]) {
              sh """
              git tag ${your_tag}
              git push https://${GIT_USERNAME}:${GIT_PASSWORD}@${repository} ${your_tag}
              git log ${GIT_PREVIOUS_COMMIT}..${GIT_COMMIT} --oneline
              """
            }

          }
        }

        stage('') {
          steps {
            sleep 12
          }
        }

      }
    }

  }
  environment {
    repository = 'github.com/binu12/pipeline-stage-when-branch.git'
    DATETIME_TAG1 = new Date().format("yyyyMMdd_HHmmss", TimeZone.getTimeZone("UTC"))
    DATETIME_TAG = DATETIME_TAG1.replaceAll(':', '_')
    your_tag = 'REL_2${DATETIME_TAG}'
  }
}
