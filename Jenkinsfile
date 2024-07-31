pipeline {
    agent any | windows
    environment { 
        CC = 'clang'
    }
        stages {
            stage('Build') {
                environment {
                    JAVA_HOME = '%JAVA_HOME%\bin'
                }
                steps {
                    bat 'windows'
                    echo 'Building'
                }
        }
    }
}