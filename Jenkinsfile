pipeline {
    agent any

    tools {
        maven 'MAVEN_HOME'
        jdk 'JAVA_LOCAL'
    }
    environment { 
        CREDS = credentials('USER_LOGIN')
    }
     options {
        buildDiscarder(logRotator(numToKeepStr: '5'))
        timeout(30)
    }
    parameters{
        string(name: 'BRANCH_NAME', defaultValue: 'main', description: 'Git branch main acesso seu no repotório')
        choice(name: 'VERSION', choices: ['17.0.13', '17.0.14', '17.0.15', '17.0.16'], description: 'Atualiza os versões')
        booleanParam(name: 'RUN_TESTS', defaultValue: true, description: 'Run tests?')
    }
    triggers {
        cron'* * * * *'
    }
        stages {
            stage('Clone'){
                steps{
                    checkout scmGit(branches: [[name: "*/${params.BRANCH_NAME}"]],  
                    userRemoteConfigs: [[credentialsId: 'jenkins_token', 
                    url: 'https://github.com/kelleao/jenkins.git']])
                           
                }
            }
            stage('Build') {
                environment{
                    NEW_VERSION = '17.0.12' 
                              
                }
                steps {
                    bat "echo versao ${NEW_VERSION}"                  
                }
            }
            stage('Test') {
                when{
                    expression{return params.RUN_TESTS}
                            
                }
                steps{
                    echo "Running tests${params.RUN_TESTS}..."
                                  
                }
            } 
            stage('Versoes'){
                    parallel{
                        stage('Git') {
                            steps {
                                bat 'git --version'
                                echo "Git versao"
                            }
                        }
                        stage('Java') {
                            steps {
                                bat 'java --version' 
                                echo "Java versao"       
                            }
                        }
                        stage('Maven') {
                            steps {
                                bat 'mvn --version' 
                                echo "Maven versao"       
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
                steps {
                    echo 'Credential...'
                    withCredentials([
                        usernamePassword(credentialsId: 'USER_LOGIN', usernameVariable: 'CREDS_USR', passwordVariable: 'CREDS_PSW')])
                        {
                            bat 'echo meu usuario e senha ${CREDS_USR} ${CREDS_PSW}'
                        }
                            echo "deploynig version ${params.VERSION}"
                            echo "O desenvolvedor escolharia main ou master: ${params.BRANCH_NAME}"
                            
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


