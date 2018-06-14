pipeline {
    agent { node { label 'linux_node' } }
    
    stages {
        stage('code-deploy') {
            
            environment 
            { 
                SHELL='/bin/sh'
        
            }
        
            steps{
            
            checkout([$class: 'GitSCM', branches: [[name: '*/master']], doGenerateSubmoduleConfigurations: false, extensions: [[$class: 'RelativeTargetDirectory', relativeTargetDir: 'pyfiles']], submoduleCfg: [], userRemoteConfigs: [[credentialsId: '7af48099-1db5-4eb9-9e1d-ffcc3d371f9f', url: 'https://github.com/kingshuk111/python.git']]])
            checkout([$class: 'GitSCM', branches: [[name: '*/master']], doGenerateSubmoduleConfigurations: false, extensions: [], submoduleCfg: [], userRemoteConfigs: [[credentialsId: '7af48099-1db5-4eb9-9e1d-ffcc3d371f9f', url: 'https://github.com/kingshuk111/shell-script.git']]])
            
	    sh """#!/bin/bash
            pwd
            cd pyfiles
            ls -lrt
            cd ..
            cp pyfiles/output.py output.py
            sh script.sh
            """
            }
          }
          }
    post {
            success{
                emailext ( 
		       subject: "Job Build", 
		       body: "Job Build Success.${env.JOB_NAME} [${env.BUILD_NUMBER}]",
		       to: "somireddypallavi@gmail.com,pallavireddy.s18995@gmail.com"
		     )
		    }

                

                 failure{
			emailext ( 
		       subject: "Job Build", 
		       body: "Job Build Success.${env.JOB_NAME} [${env.BUILD_NUMBER}]",
		       to: "somireddypallavi@gmail.com,pallavireddy.s18995@gmail.com"
		     )
		     }

        }
        
    }
