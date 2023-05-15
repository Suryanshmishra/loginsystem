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
    stage('Build') {
          steps { 
                   
              sh """#!/bin/bash
                #Build stage 
                echo "This project No Need any Build like Java and Dot net"
                """
            
          }
    }
    
    
     stage('Unit test') {
          steps { 
                   
              sh """#!/bin/bash
                #Unit test stage 
                echo "If any unit test realated to project we can put cases here"
                """
            
          }
    }
    
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
                
                cp -r ./loginsystem /www/wwwroot/loginystem.com/loginsystem/
                
                #cp -r ./loginsystem /www/wwwroot/loginsystem/
                """
            
          }
    }
     stage('Automation testing') {
          steps { 
                   
              sh """#!/bin/bash
                #Build stage 
                echo "automation can be done using selenium script  "
                """
            
          }
    }
  } 
}
