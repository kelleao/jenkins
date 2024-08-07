pipeline {
    agent any

    environment { 
        NEW_VERSION = '17.0.12'
        CREDS = credentials('USER_LOGIN')
    }

     options {
        buildDiscarder(logRotator(numToKeepStr: '1'))
        timeout(30)
    }

    //  parameters {
    //     credentials credentialType: 'com.cloudbees.plugins.credentials.impl.UsernamePasswordCredentialsImpl', 
    //     defaultValue: 'USER_LOGIN', 
    //     description: 'Meu usuario e senha acessa github.', 
    //     name: 'USER_LOGIN', 
    //     required: true
    // }

    parameters{
        choice(name: 'VERSION', choices: ['17.0.13', '17.0.14', '17.0.15', '17.0.16'], description: '')
        booleanParam(name: 'executeTests', defaultValue: true, description: '')
    }

    triggers {
        cron('H */4 * * 1-5')
    }

        stages {
            stage('Build') {
                steps {

                    bat '${env.NEW_VERSION}'
                    
                    // bat 'echo meu user ${CREDS_USR}'
                    // bat 'echo minha senha ${CREDS_PSW}'
                   
                }
            }
                // stage('Parameters credenciais') {
                //     steps {
                //        bat "echo '${params.USER_LOGIN}'"
                //     }
                // }
                
                stage('Test') {
                    when{
                        expression{
                            params.executeTests
                        }
                    }
                    steps{
                     echo 'Running unit tests...'
                     
                     
                    }
                }    
                
                stage('Deploy') {
                    steps {
                        echo 'deplying the application...'
                        withCredentials([
                            usernamePassword(credentials: 'USER_LOGIN', usernameVariable: CREDS_USR, passwordVariable: CREDS_PSW)
                        ]){
                            bat "Meu user ${CREDS_USR} minha senha ${CREDS_PSW}"
                        }

                        echo "deploynig version ${params.VERSION}"
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
   



