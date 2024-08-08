pipeline {
    agent any
    environment { 
        NEW_VERSION = '17.0.12'
        CREDS = credentials('USER_LOGIN')
    }
     options {
        buildDiscarder(logRotator(numToKeepStr: '1'))
        parallelsAlwaysFailFast()
        timeout(30)
    }
    parameters{
        choice(name: 'VERSION', choices: ['17.0.13', '17.0.14', '17.0.15', '17.0.16'], description: '')
        booleanParam(name: 'executeTests', defaultValue: true, description: '')
    }
    triggers {
        cron('H */4 * * 1-5')
    }
        stages {
            stage('Clone'){
                steps{
                    git branch: 'main', url: 'https://github.com/kelleao/jenkins.git'
                }
            }
            stage('Build') {
                steps {
                    echo "versao ${NEW_VERSION}"              
                }
            }
                stage('Test') {
                    when{
                        
                        expression{
                            branch 'main'
                            environment name: 'Git', value: 'main'
                            params.executeTests
                        }
                    }
                    steps{
                     echo 'Running tests...'
                     echo "${Git}"
                     
                    }
                } 
                stage('Deploy') {                    
                        steps {
                            echo 'deplying the application...'
                            withCredentials([
                                usernamePassword(credentialsId: 'USER_LOGIN', usernameVariable: 'CREDS_USR', passwordVariable: 'CREDS_PSW')
                            ]){
                                bat 'echo meu usuario e senha ${CREDS_USR} ${CREDS_PSW}'
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


   



