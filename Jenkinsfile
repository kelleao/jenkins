pipeline {
    agent any

    environment { 
       GIT_URL = 'https://github.com/kelleao/jenkins'
    }
    

        stages {
            stage('Build') {
                steps {
                  checkout scmGit(branches: [[name: 'main']], 
                    browser: github('${GIT_URL}'), 
                    extensions: [cloneOption(honorRefspec: true, 
                    noTags: true, reference: '', shallow: false), lfs(), 
                    localBranch('main')], 
                    userRemoteConfigs: [[url: '${GIT_URL}']])
                }
        }
            
    }
}


