pipeline {
    agent any

    environment { 
       GIT_URL = 'https://github.com/kelleao/jenkins'
    }
    

        stages {
            stage('Build') {
                steps {
                 git branch: 'main', credentialsId: '7fd00f8d-feec-43f5-a65e-4cd72c90262c', url: '${env.GIT_URL}'
                }
        }
            
    }
}


