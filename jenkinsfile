pipeline {
    agent any
    
    stages {
        stage('code-deploy') {
            
            environment 
            { 
                SHELL=/bin/sh
        
            }
        
            steps{
            
            checkout([$class: 'GitSCM', doGenerateSubmoduleConfigurations: false, extensions: [], submoduleCfg: [], userRemoteConfigs: [url: 'https://github.com/kingshuk111/shell-script.git','https://github.com/kingshuk111/python.git']]) 
            sh """#!/bin/bash -xel
            
            echo "**************************************Deployment Starts *************************************************"
            
            echo "**************************************Deployment Ends ***************************************************"
            """
            }
          }
    
    post {
            success{
                emailext ( 
		       subject: "Job Build", 
		       body: "Job Build Success.${env.JOB_NAME} [${env.BUILD_NUMBER}]",
		       to: "pallavireddy.s18995@gmail.com"
		     )
		    }

                

                 failure{
			emailext ( 
		       subject: "Job Build", 
		       body: "Job Build Success.${env.JOB_NAME} [${env.BUILD_NUMBER}]",
		       to: "pallavireddy.s18995@gmail.com"
		     )
		     }

        }
        
    }

}
