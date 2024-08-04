pipeline {
    agent any

    environment { 
      GIT_URL = 'https://github.com/kelleao/jenkins'
        //GIT_HUB with  <username>:<password>
        //GIT_HUB_ACCESS_KEY_ID     = credentials('jenkins-aws-secret-key-id')
        //GIT_HUB_SECRET_ACCESS_KEY = credentials('jenkins-aws-secret-access-key')
    }
    
    // parameters {
    //     string(name: 'STATEMENT', defaultValue: 'hello; ls /', description: 'What should I say?')
    // }
        stages {
            stage('Build Git-URL') {
                steps {
                 bat ' \'"git branch: \\\'main\\\', url: "${env.GIT_URL}" "\''
                 echo 'Git URl'
                }
        }
            
    }
   
}


