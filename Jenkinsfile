pipeline {
  agent any
    environment {
        name_final = "ams/country:${currentBuild.number}"        
    }
    stages {
        stage('build') {
            steps {
                script{
                    sh ''' 
                    docker build -t ${name_final} .
                    '''
                    }
                }                    
            }
          
        }   
    }