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
                    environment { 
                     SERVICE_CREDS = credentials('my-predefined-username-password') 
                }
                    steps {
                        bat 'echo "Service user is $SERVICE_CREDS_USR"'
                        bat 'echo "Service password is $SERVICE_CREDS_PSW"'
                    }
                    
                }
            }

            post { 
                always { 
                    echo 'I will always say Hello again!'
                }
                failure {
                mail to: team@example.com, subject: 'The Pipeline failed :('
            }
            success {
                echo 'I will sucess say Hello again!'
            }
        }
                
    }
        
            
}
   



