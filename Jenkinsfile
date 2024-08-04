pipeline {
    agent any

    environment { 
      GIT_URL = 'https://github.com/kelleao/jenkins'
        //GIT_HUB with  <kelleao>:<password>
        
    }
     options {
        disableConcurrentBuilds(abortPrevious: env.GIT_URL != null)
        timeout(time: 1, unit: 'SECONDS')
    }
    parameters {
        string(name: 'GIT_URL', defaultValue: "https://github.com/kelleao/jenkins.git", , description: 'Acesso do Github URL no branch')
    }
        stages {
            stage('Build') {
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
                        echo "${params.GIT_URL}"
                    }
            }

            stage('Test') {
                steps {
                    bat 'make check'
                }
            }
            stage('Deploy') {
                steps {
                  
                  
            }
        }
        post { 
                always { 
                    echo 'I will always say Hello again!'
                }
                
    }
        
            
}
   



