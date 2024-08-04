pipeline {
    agent any

    environment { 
       GIT_URL = 'https://github.com/kelleao/jenkins'
    }

        stages {
            stage('Build') {
                steps {
                   git branch: 'main' URL: '${GIT_URL}'
                }
        }
            stage('Test') {
                steps {
                    echo 'Testing..'
                }
            }
    }
}