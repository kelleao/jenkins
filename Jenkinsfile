pipeline {
    agent any

    environment { 
      CREDS = credentials('github-key')
    }

     options {
        buildDiscarder(logRotator(numToKeepStr: '1'))
        timeout(30)
    }

     parameters {
        credentials credentialType: 'com.cloudbees.plugins.credentials.impl.UsernamePasswordCredentialsImpl', 
        defaultValue: 'github-key', 
        description: 'Meu usuario e senha acessa github.', 
        name: 'github-key', 
        required: true
    }

    triggers {
        cron('H */4 * * 1-5')
    }

        stages {
            stage('Build') {
                steps {
                    bat 'echo meu user ${CREDS_USR}'
                    bat 'echo minha senha ${CREDS_PSW}'
                }
            }
                stage('Parameters credenciais') {
                    steps {
                       bat "echo '${params.github-key}'"
                    }
                }
                
                stage('Test') {
                    steps{
                     echo 'unit tests'
                    }
                }    
                
                stage('Deploy') {
                    when {
                     branch 'main'
                     environment name: 'DEPLOY_TO', value: 'main'
                    }
                    steps {
                        echo '${DEPLOY_TO}'
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
   



