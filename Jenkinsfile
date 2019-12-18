pipeline {
    agent any
       environment { 
        repository = "github.com/binu12/pipeline-stage-when-branch.git"
                your_tag = "REL_2_0_0"
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
                withCredentials([usernamePassword(credentialsId: GIT_CREDS, passwordVariable: 'GIT_PASSWORD', usernameVariable: 'GIT_USERNAME')]) {
                   sh("""
                        git config --global credential.username {GIT_USERNAME}
                        git config --global credential.helper "!echo password={GITPASSWORD}; echo"
                        git tag -d ${your_tag}
                        git tag ${your_tag}
                        git push origin ${your_tag}
                    """)
  
                }
            }
            
        }
        
    }
}
