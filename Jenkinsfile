pipeline {
    agent any    
       environment { 
        repository = "github.com/binu12/pipeline-stage-when-branch.git"
           DATETIME_TAG = new Date().format("yyyy-MM-dd'T'HH:mm:ss'Z'", TimeZone.getTimeZone("UTC"))
           DATETIME_TAG = DATETIME_TAG.replaceAll(':', '_')
           your_tag = "REL_2" + '${DATETIME_TAG}'
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
                withCredentials([usernamePassword(credentialsId: '00d1ed86-e252-4171-97e6-c69de2b7ac90', passwordVariable: 'GIT_PASSWORD', usernameVariable: 'GIT_USERNAME')]) {
                   sh("""
                       
                        git tag ${your_tag}
                        git push https://${GIT_USERNAME}:${GIT_PASSWORD}@${repository} ${your_tag}
                    """)
  
                }
            }
            
        }
        
    }
}
