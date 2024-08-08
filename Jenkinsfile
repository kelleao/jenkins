pipeline {
    agent any

    tools {
        maven 'MAVEN_HOME'
        jdk 'JAVA_LOCAL'
    }
    environment { 
        NEW_VERSION = '17.0.12'
        CREDS = credentials('USER_LOGIN')
        DEPLOY_ENV = 'staging'
    }
     options {
        buildDiscarder(logRotator(numToKeepStr: '1'))
        parallelsAlwaysFailFast()
        timeout(30)
    }
    parameters{
        string(name: 'BRANCH_NAME', defaultValue: 'main', description: 'Branch to build')
        choice(name: 'VERSION', choices: ['17.0.13', '17.0.14', '17.0.15', '17.0.16'], description: '')
        booleanParam(name: 'RUN_TESTS', defaultValue: true, description: 'Run tests?')
    }
    triggers {
        cron'* * * * *'
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
                    bat 'mvn --version'     
                    bat 'java --version'        
                }
            }
                stage('Test') {
                    when{
                        expression{return params.RUN_TESTS}
                            
                    }
                    steps{
                     echo 'Running tests...'
                     bat 'make check || true'              
                    }
                } 
                stage('parallel test'){
                    when {
                        branch 'main'
                    }
                        parallel{
                            
                        stage('Branch Github') {
                                steps {
                                    echo "On Branch A"
                                }
                            }
                            stage('Branch Gitlab') {
                                steps {
                                    echo "On Branch B"
                                }
                            }
                    }
                }
                stage('Deploy') {
                     when {
                        allOf {
                            expression { return params.BRANCH_NAME == 'main' }
                            expression { currentBuild.result == null || currentBuild.result == 'SUCCESS' }
                        }
                    }
                        //input message: "Does http://localhost:8888/staging/ look good?"                    
                        steps {
                            echo 'Credential...'
                            withCredentials([
                                usernamePassword(credentialsId: 'USER_LOGIN', usernameVariable: 'CREDS_USR', passwordVariable: 'CREDS_PSW')
                            ]){
                                bat 'echo meu usuario e senha ${CREDS_USR} ${CREDS_PSW}'
                            }

                            echo "deploynig version ${params.VERSION}"
                            echo "Deploying to ${env.DEPLOY_ENV}..."
                        }
                        
                }
            }

            post { 
                always {
                echo "Cleaning up..."  
            }
                success {
                    echo 'Build succeeded!'
                }
                failure {
                    echo 'Build failed!'
                }
                
        }
    }


