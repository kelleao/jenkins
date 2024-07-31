pipeline {
    agent any 
    environment { 
        CC = 'clang'
    }
     options {
        buildDiscarder(10)
        timeout(30) 
    }
        stages {
            stage('Build') {
                environment {
                    JAVA_HOME = '%JAVA_HOME%\bin'
                }
                steps {
                     bat 'echo "java ambiente is $JAVA_HOME"'
                }
        }
    }
}