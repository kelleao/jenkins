pipeline {
    agent any

    environment { 
      GIT_URL = 'https://github.com/kelleao/jenkins'
        //GIT_HUB with  <kelleao>:<password>
        
    }
     options {
    skipDefaultCheckout()
    }
    parameters {
        gitParameter branchFilter: 'origin/(.*)', defaultValue: 'main', name: 'BRANCH', type: 'PT_BRANCH'
    }
        stages {
            stage('Pré-Build Git-URL') {
                steps {
                    git branch: 'main', url: "${env.GIT_URL}"
                    echo 'Git URl'
                }
        }
        stage('Parameters Git repositorio') {
                steps {
                     git branch: "${params.BRANCH}", url: '${env.GIT_URL}'
                }
        }
            
    }
        
            
}
   



