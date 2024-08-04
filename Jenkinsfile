pipeline {
    agent any

    environment { 
       URL = 'https://github.com/kelleao/jenkins'
    }
    

        stages {
            stage('Build') {
                steps {
                  git branch: 'main', url: "${URL}"
                }
        }
            
    }
}


