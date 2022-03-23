pipeline {
    agent { label 'slave1' }

    

    stages {
         stage('Setup parameters1') {
            steps {
                script { 
                    properties([
                        parameters([
                            choice(
                                choices: ['UACC', 'PROD'], 
                                name: 'ENVIRONMENT'
                            )
                             ])
                              ])
                }
            }
         }
        
            
         
stage('deploy Production') {
           when {
                expression { 
                   return params.ENVIRONMENT == 'PROD'
                }
            }
            steps 
            {
                script
                {
                    def userInput = input(id: 'userInput', message: 'Let\'s promote?(yes/no)', parameters: [[$class: 'TextParameterDefinition', defaultValue: 'yes', description: 'prom', name: 'prom']])
                    if (userInput != "yes"){
                        currentBuild.result = 'FAILURE'
                        error("Stopping early!")
                    }
                    
                }
            
            
            
            
                
                    
                    sh "scp -o StrictHostKeyChecking=no /etc/systemd/system/npm.service root@10.66.24.184:/etc/systemd/system"
                    sh "systemctl daemon-reload"
                    sh "systemctl start npm.service"
                    sh "systemctl status npm.service"
                    echo "deploy to PROD"
                    """
                                    
                
            }
}
            
   stage('Deploy to UACC') {
            when {
                expression { 
                   return params.ENVIRONMENT == 'UACC'
                }
            }
            steps {
                 sh "mydev=$(curl --request GET http://10.66.24.183:8500/v1/kv/dev |jq .[0]."Value" -r | base64 --decode)&&scp -o StrictHostKeyChecking=no root@$mydev:/develop/scala3-example-project_3-0.1.0.jar /tmp"
                 sh "myuacc=$(curl --request GET http://10.66.24.183:8500/v1/kv/uacc |jq .[0]."Value" -r | base64 --decode)scp -o StrictHostKeyChecking=no /tmp/scala3-example-project_3-0.1.0.jar root@$myuacc:/uacc"

                    sh """
                    echo "deploy to UACC"
                    """
                }
            }
   
        }
    
    }
