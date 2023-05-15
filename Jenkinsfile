pipeline {
  agent any

  environment {
    
    WORKSPACE           = '.'
    DBRKS_BEARER_TOKEN  = "xyz"
    DBTOKEN             ="DBTOKEN"
    CLUSTERID           ="1228-220746-bqqkddxs"
    DBURL               ="https://adb-6840195589605290.10.azuredatabricks.net"

    TESTRESULTPATH  ="./teste_results"
    LIBRARYPATH     = "./Libraries"
    OUTFILEPATH     = "./Validation/Output"
    NOTEBOOKPATH    = "./Notebooks"
    WORKSPACEPATH   = "/Shared"
    DBFSPATH        = "dbfs:/FileStore/"
    BUILDPATH       = "${WORKSPACE}/Builds/${env.JOB_NAME}-${env.BUILD_NUMBER}"
    SCRIPTPATH      = "./Scripts"
  }

  stages {
    
    stage('Build Artifact') {
        steps {
            sh "printenv | sort"
            sh """mkdir -p "${BUILDPATH}/Workspace"
              
              
              cp -r ./loginsystem ${BUILDPATH}/Workspace
    

              # Generate artifact
              tar -czvf ./latest_build"${env.BUILD_NUMBER}".tar.gz ${BUILDPATH}
              cp ./latest_build"${env.BUILD_NUMBER}".tar.gz ./Builds
           """
        }

    }

    stage('Deploy') {
          steps { 
                   
              sh """#!/bin/bash
                
                cp -r ./loginsystem /www/wwwroot/loginsystem/
                """
            
          }
    }
  } 
}
