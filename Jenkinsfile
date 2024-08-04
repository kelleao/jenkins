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
        string(name: 'Kelleao', defaultValue: '${env.GIT_URL}', description: 'Acesso o Git no repositório?')
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
                     git branch: 'main', url: "${params.GIT_URL}"
                }
        }
            
    }
        
            
}
   



