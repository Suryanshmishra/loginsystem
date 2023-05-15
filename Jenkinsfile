pipeline {
  agent any

  environment {
    
    WORKSPACE           = '.'
    
    TESTRESULTPATH  ="./teste_results"
    WORKSPACEPATH   = "/Shared"
    DBFSPATH        = "dbfs:/FileStore/"
    BUILDPATH       = "${WORKSPACE}/Builds/${env.JOB_NAME}-${env.BUILD_NUMBER}"
    BACKUPATH      = "/var/lib/jenkins/workspace/backup"
  }

  stages {
    
    stage('Build Artifact') {
        steps {
            sh "printenv | sort"
            sh """mkdir -p "${BUILDPATH}/Workspace"
              
              #copy on builds path
              cp -r ./loginsystem ${BUILDPATH}/Workspace
    

              # Generate artifact
              tar -czvf ./latest_build"${env.BUILD_NUMBER}".tar.gz ${BUILDPATH}
              
              # backup of Code
              cp ./latest_build"${env.BUILD_NUMBER}".tar.gz ${BACKUPATH}
           """
        }

    }

    stage('Deploy') {
          steps { 
                   
              sh """#!/bin/bash
                #Deployment of code on live server
                cp -r ./loginsystem /www/wwwroot/loginsystem/
                """
            
          }
    }
  } 
}
