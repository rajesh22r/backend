pipeline {
    agent {
        label 'AGENT-1'
    
    }
   
    options{
        timeout( time: 30, unit: 'MINUTES')
        disableConcurrentBuilds()
    }
    environment{
        DEBUG = 'true'
        appVersion = '' //global can use across
    }
    stages {
        stage('Read the version ') { 
            steps {
              script{
                def packageJson = readJSON file: 'package.json'
                appVersion = packageJson.version
                echo "AppVersion : ${appVersion} "
              }
              
            }
        }
        stage('install dependencies') { 
            steps {
               sh   'npm install'
               
            }
        }
        stage('Docker build') { 
            
            steps {
                sh """
                docker build -t joindevops/backend:${appVersion} .
                docker images


                """
                
            }
        }
        stage('print params') { 
            steps {
                echo " Hello ${params.PERSON}"
                echo " biography: ${params.BIOGRAPHY}"
                echo "Toggle: ${params.TOGGLE}"

                echo "Choice: ${params.CHOICE}"

                echo "Password: ${params.PASSWORD}"
                
            }
        }
         
         
        // stage('Approval') {
        //     input {
        //         message "Should we continue?"
        //         ok "Yes, we should."
        //         submitter "alice,bob"
        //         parameters {
        //             string(name: 'PERSON', defaultValue: 'Mr Jenkins', description: 'Who should I say hello to?')
        //         }
        //     }
        //     steps {
        //         echo "Hello, ${PERSON}, nice to meet you."
        //     }
        // }
    
    }
        post { 
        always { 
            deleteDir()
        }
        success{
             
             echo 'this section runs when pipeline success'
         }
        failure{
             echo 'this section runs when pipeline failure'
        }
    }

}