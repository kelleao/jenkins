pipeline {
    agent any

    environment { 
      GIT_URL = 'https://github.com/kelleao/jenkins'
      CREDS = credentials('USER_TEST')
    }
     options {
        buildDiscarder(logRotator(numToKeepStr: '1'))
        timeout(30)
    }
     parameters {
        credentials credentialType: 'com.cloudbees.plugins.credentials.impl.UsernamePasswordCredentialsImpl', 
        defaultValue: 'USER_LOGIN', 
        description: 'Meu usuario e senha acessa github.', 
        name: 'USER_LOGIN', 
        required: true
    }

    // triggers {
    //     cron('H */4 * * 1-5')
    // }
        stages {
            stage('Build') {
                steps {
                    git branch: 'main', url: "${env.GIT_URL}"
                    echo 'Git URl'
                }
        }
            stage('Parameters credenciais') {
                    steps {
                        git branch: 'main', url: "${params.USER_LOGIN}"
                    }
            }
            stage('Credenciais my usr e psw') {
                 bat 'echo meu user ${CREDS_USR}'
                 bat 'echo minha senha ${CREDS_PSW}'
            }
            
            stage('Test') {
               bat 'echo Running unit tests'
        }    
            stage('Deploy') {
                    when {
                    branch 'main'
                    environment name: 'DEPLOY_TO', value: 'main'
                }
                steps {
                   bat 'echo ${DEPLOY_TO}'
                }
            }    
    }

    post { 
        always { 
            echo 'I will always say Hello again!'
        }
        success {
            echo 'Only on SUCCESS'
        }
        failure {
            echo 'Only on Failure'
        }
        unstable {
            echo 'Only if run is unstable'
        }
        changed {
            echo 'Only if status changed from Success to Failure or vice versa w.r.t. last run.'
        }
    }
}
   



