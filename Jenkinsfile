pipeline {
    agent any

    environment { 
       JENKINS_URL = 'https://github.com/kelleao/jenkins'
    }
    

        stages {
            stage('Build') {
                steps {
                  git branch: 'main', url: "${env.JENKINS_URL}" 
                }
        }
            
    }
}


