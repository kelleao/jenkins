pipeline {
    agent any

    environment { 
       GIT_HUB = 'https://github.com/kelleao/jenkins'
        //GIT_HUB with  <username>:<password>
    }
    

        stages {
            stage('Build') {
                steps {
                  git branch: 'main', url: "${env.GIT_HUB}" 
                }
        }
            
    }
}


