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
                
                emailext  attachmentsPattern: '', body: '''<html>
                <body>
                <h1 style="color:blue;"> BUILD SUCCESSFULL </h1>
                <table>
                        
                        <tr>
                            <td >Jenkins  URL</td>
                            <td>:</td>
                            <td >$JENKINS_URL</td>
                        </tr>
                        <tr>
                            <td >Job Name</td>
                            <td>:</td>
                            <td >$JOB_NAME</td>
                        </tr>
                        <tr>
                            <td >Build Number</td>
                            <td>:</td>
                            <td >$BUILD_NUMBER</td>
                        </tr>
                        
                        
		</table>
                  <h1 style="color:blue;"> CONSOLE LOG OUTPUT</h1>
                  <pre>${BUILD_LOG, maxLines=8000, escapeHtml=true}</pre>
                  </body>
                  </html>''', mimeType: 'text/html', subject: 'core.deploy pipeline ', to: 'pallavireddy.s18995@gmail.com'

                }

                 failure{

                     emailext  attachmentsPattern: '', body: '''<html>
                  <body>
                  <h1 style="color:red;"> BUILD FAILED </h1>
                     <table>
                        
                        <tr>
                            <td >Jenkins  URL</td>
                            <td>:</td>
                            <td >$JENKINS_URL</td>
                        </tr>
                        <tr>
                            <td >Job Name</td>
                            <td>:</td>
                            <td >$JOB_NAME</td>
                        </tr>
                        <tr>
                            <td >Build Number</td>
                            <td>:</td>
                            <td >$BUILD_NUMBER</td>
                        </tr>
                        
                        
		</table>
                  <h1 style="color:pink;"> CONSOLE LOG OUTPUT</h1>
		     }
                  <pre>${BUILD_LOG, maxLines=8000, escapeHtml=true}</pre>
                  </body>
                 </html>''', mimeType: 'text/html', subject: 'core.deploy pipeline', to: 'pallavireddy.s18995@gmail.com'

        }
    } 
    }
