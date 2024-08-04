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
        string(name: 'GIT_URL', defaultValue: "GIT_URL", , description: 'Acesso do Github URL no branch')
    }
        stages {
            stage('Build Git-URL') {
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
        stage('Acesso Git repositorio') {
                steps {
                     echo "${params.URL}"
                }
        }
            
    }
        
            
}
   



