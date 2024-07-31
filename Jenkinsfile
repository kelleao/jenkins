pipeline {
    agent any 
    environment { 
        CC = 'clang'
    }
        stages {
            stage('Build') {
                environment {
                    JAVA_HOME = '%JAVA_HOME%\bin'
                }
                steps {
                    echo 'Building'
                }
        }
    }
}