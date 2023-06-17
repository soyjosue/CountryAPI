pipeline {
  agent any
    environment {
        name_final = "ams/country:${currentBuild.number}"        
    }
    stages {
        stage('Branch name')
        {
            steps {
                echo "${env.BRANCH_NAME}"

                sh '''
                    printenv
                '''
            }
        }

        stage('Get GITVERSION')
        {
            steps {
                script {
                    def props = readProperties file: 'gitversion.properties'

                    env.GitVersion_SemVer = props.GitVersion_SemVer
                    env.GitVersion_FullSemVer = props.GitVersion_FullSemVer
                    env.GitVersion_BranchName = props.GitVersion_BranchName
                    env.GitVersion_AssemblySemVer = props.GitVersion_AssemblySemVer
                    env.GitVersion_MajorMinorPatch = props.GitVersion_MajorMinorPatch
                    env.GitVersion_Sha = props.GitVersion_Sha
                }
            }
        }

        stage('build') {
            steps {
                script{
                    sh ''' 
                    docker build -t ams/country:${env.GitVersion_FullSemVer} .
                    '''
                    }
                }                    
            }
          
        }   
    }