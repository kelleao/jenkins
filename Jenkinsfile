pipeline {
    agent any 
    environment { 
        CC = 'clang'
    }
     options {
        buildDiscarder(logRotator(numToKeepStr: '1'))
        timeout(10) 
    }
        stages {
            stage('Build') {
                environment {
                    JAVA_HOME = '%JAVA_HOME%\bin'
                    JENKINS_URL = 'http://localhost:8080/'
                }
                steps {
                     bat 'echo "java ambiente is $JAVA_HOME"'
                }
        }
    }
}