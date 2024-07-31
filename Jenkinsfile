pipeline {
    agent any

    environment { 
       JAVA_HOME = '%JAVA_HOME%\bin'
       JENKINS_URL = 'http://localhost:8080/'
    }
     options {
        buildDiscarder(logRotator(numToKeepStr: '1'))
        timeout(10) 
    }
        stages {
            stage('Build') {
                steps {
                    bat 'echo "java ambiente is ${JAVA_HOME}"'
                    bat 'echo "Acesso URL is ${JENKINS_URL}"'
                }
        }
            stage('Test') {
                steps {
                    echo 'Testing..'
                }
            }
    }
}