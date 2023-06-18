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

        stage('master')
        {
            when {
                branch "main"
            }
            steps {
                echo "${env.BRANCH_NAME}"
                echo "${BRANCH_NAME}"

                sh '''
                    printenv
                    /root/.dotnet/tools/dotnet-gitversion /output buildserver
                '''

                echo "This is Master branch Execution"
                script {
                    def props = readProperties file: 'gitversion.properties'

                    env.GitVersion_SemVer = props.GitVersion_SemVer
                    env.GitVersion_FullSemVer = props.GitVersion_FullSemVer
                    env.GitVersion_BranchName = props.GitVersion_BranchName
                    env.GitVersion_AssemblySemVer = props.GitVersion_AssemblySemVer
                    env.GitVersion_MajorMinorPatch = props.GitVersion_MajorMinorPatch
                    env.GitVersion_Sha = props.GitVersion_Sha

                    echo env.GitVersion_SemVer
                    echo env.GitVersion_MajorMinorPatch
                    echo env.GitVersion_FullSemVer

                }
            }
        }

        stage('major')
        {
            when {
                branch "major-*"
            }
            steps {
                echo "${env.BRANCH_NAME}"
                echo "${BRANCH_NAME}"

                sh '''
                    printenv
                    /root/.dotnet/tools/dotnet-gitversion /output buildserver
                '''

                echo "This is major branch Execution"
                script {
                    def props = readProperties file: 'gitversion.properties'

                    env.GitVersion_SemVer = props.GitVersion_SemVer
                    env.GitVersion_FullSemVer = props.GitVersion_FullSemVer
                    env.GitVersion_BranchName = props.GitVersion_BranchName
                    env.GitVersion_AssemblySemVer = props.GitVersion_AssemblySemVer
                    env.GitVersion_MajorMinorPatch = props.GitVersion_MajorMinorPatch
                    env.GitVersion_Sha = props.GitVersion_Sha

                    echo env.GitVersion_SemVer
                    echo env.GitVersion_MajorMinorPatch
                    echo env.GitVersion_FullSemVer

                }
            }
        }

        stage('Feature')
        {
            when {
                branch "feature-*"
            }
            steps {
                echo "${env.BRANCH_NAME}"
                echo "${BRANCH_NAME}"

                sh '''
                    printenv
                    /root/.dotnet/tools/dotnet-gitversion /output buildserver
                '''

                echo "This is feature branch Execution"
                script {
                    def props = readProperties file: 'gitversion.properties'

                    env.GitVersion_SemVer = props.GitVersion_SemVer
                    env.GitVersion_FullSemVer = props.GitVersion_FullSemVer
                    env.GitVersion_BranchName = props.GitVersion_BranchName
                    env.GitVersion_AssemblySemVer = props.GitVersion_AssemblySemVer
                    env.GitVersion_MajorMinorPatch = props.GitVersion_MajorMinorPatch
                    env.GitVersion_Sha = props.GitVersion_Sha

                    echo env.GitVersion_SemVer
                    echo env.GitVersion_MajorMinorPatch
                    echo env.GitVersion_FullSemVer

                }
            }
        }

        stage('build') {
            steps {
                sh "docker build -t ams/country:${env.GitVersion_FullSemVer} ."
            }
          
        }   
    }
}