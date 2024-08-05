pipeline {
    agent any

    environment { 
      GIT_URL = 'https://github.com/kelleao/jenkins'
        //GIT_URL with  <user_login>:<password>
    }
     options {
        buildDiscarder(logRotator(numToKeepStr: '1'))
        timeout(30)
    }
    parameters {
        string(name: 'GIT_URL', defaultValue: "https://github.com/kelleao/jenkins.git", , description: 'Acesso do Github URL no branch')
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
                input{
                    message "Devemos continuar"
                    ok "Yes, dever."
                    submitter "raquel, leao"

                    parameters {
                    string(name: 'URL', defaultValue: 'Jenkins', description: 'Para quem devo dizer olá?')
                }
                }
                steps {
                    echo "Olá, ${params.URL}, faço implementar a pipeline do Jenkins."
                }
        }    
            stage('Deploy') {
                    when {
                    branch 'main'
                    environment name: 'DEPLOY_TO', value: 'main'
                }
                steps {
                   bat "echo ${DEPLOY_TO}"
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
   



