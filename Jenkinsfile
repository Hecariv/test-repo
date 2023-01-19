@Library('Codebeamer-CI@ALM-12241') _
def changeSet = []
pipeline {
    agent any
  
    stages{  
        
           stage('Check ChangeSet') {
            when {
                anyOf {
                    not {
                        anyOf {
                            changeset "**/*content.y*ml"
                            changeset "**/*release.y*ml"
                        }
                    }
                    allOf {
                        changeset "**/*content.y*ml"
                        changeset "**/*release.y*ml"
                    }
                }
                
            }
            steps {
                 script {
                    currentBuild.result = "FAILURE"
                    error("Not Allow")
                 }
                }
        }
    
        stage('Configuration') {
            when { 
                changeset pattern:"**/*content.y*ml", caseSensitive: false
            }
            steps {
                sh "echo 'Configuration'"
                getChangeFiles()
                getChangeFiles()
            }
        }

        stage('Deployment') {
            when { 
                changeset pattern:"**/*release.y*ml" , caseSensitive: false
            }
            steps {
                sh "echo 'Deployment'"
                deployProject(changeSet, env.BRANCH_NAME)
            }
        }
    }
     post { 
        always { 
            cleanWs()
        }
    }
}
