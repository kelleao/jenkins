pipeline {
    agent any

    environment { 
       GIT_URL = 'https://github.com/kelleao/jenkins'
    }
    

        stages {
            stage('Build') {
                steps {
                  GIT_URL = '${GIT_URL}'
                }
        }
            
    }
}


