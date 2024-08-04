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
        gitParameter defaultValue: 'main', name: 'BRANCH'
    }
        stages {
            stage('Pre-Build Git-URL') {
                steps {
                    git branch: 'main', url: "${env.GIT_URL}"
                    echo 'Git URl'
                }
        }
        stage('Parameters Git repositorio') {
                steps {
                     git branch: "${params.BRANCH}", url: 'https://github.com/kelleao/jenkins.git'
                }
        }
            
    }
        
            
}
   



