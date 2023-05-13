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
            sh """mkdir -p "${BUILDPATH}/Workspace"
              mkdir -p "${BUILDPATH}/Libraries/python"
              mkdir -p "${BUILDPATH}/Validation/Output"
              
              cp ${WORKSPACE}/Workspace/*.ipynb ${BUILDPATH}/Workspace
    
              # Get packaged libs
              find ${LIBRARYPATH} -name '*.whl' | xargs -I '{}' cp '{}' ${BUILDPATH}/Libraries/python/

              # Generate artifact
              #tar -czvf Builds/latest_build.tar.gz ${BUILDPATH}
           """
        }

    }

    stage('Deploy') {
          steps { 
            withCredentials([string(credentialsId: DBTOKEN, variable: 'TOKEN')]) {        
              sh """#!/bin/bash
                source $WORKSPACE/miniconda/etc/profile.d/conda.sh
                conda activate mlops2
                export PATH="$HOME/.local/bin:$PATH"


                # Use Databricks CLI to deploy notebooks
                databricks workspace import_dir --overwrite ${BUILDPATH}/Workspace ${WORKSPACEPATH}
                dbfs cp -r ${BUILDPATH}/Libraries/python ${DBFSPATH}
                """
            }
          }
    }
  } 
}
