pipeline {
    agent any
       environment { 
        repository = "https://github.com/binu12/pipeline-stage-when-branch.git"
                your_tag = "REL_1_0_0"
       }
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
            steps {
                withCredentials([usernamePassword(credentialsId: '5ce6e7ce-9748-4f00-81f7-8fbd8d8018cb', passwordVariable: 'GIT_PASSWORD', usernameVariable: 'GIT_USERNAME')]) {
                  sh "git tag ${your_tag}"
                  sh "git push origin ${your_tag}"
                }
            }
            
        }
        
    }
}
