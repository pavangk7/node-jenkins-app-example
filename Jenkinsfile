pipeline {
  agent {
           node {
                label 'Linux-commercial'
            }
  }
  parameters{
        choice(name: "ENV", choices: ["Dev", "PVE", "PV", "PE", "PROD"], description: " multi-choice parameter Pipeline")
  }  
     
  stages {
        
            
    stage('Build & Publish') {
      steps {
        script {
        switch(env.ENV) {
            case 'Dev':
              sh 'npm  run build-dev'
              break
            case 'PV':
              sh 'npm  run build-py'
              break
            case 'PE':
              sh 'npm run build-pe'
              break
            case 'PROD':
              sh 'npm run build-production'
              break
                        
        }
        }
                
        }

        post {
                success {
                    
                    rtUpload (
                      serverId: "main",
                      spec:
                          """{
                            "files": [
                              {
                                "pattern": "dist/nssp-ui/folder",
                                "target": "Commercial_Releases/nssp-ui/$params.ENV/${BUILD_ID}/"
                              }
                            ]
                          }""",
                    failNoOp: true 
                    ) 
                }

                    
                }
            }
    } 
}
