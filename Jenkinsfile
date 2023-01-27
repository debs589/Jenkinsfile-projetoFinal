pipeline {
    agent any
    stages {
        stage('Clone repository') { 
            steps {
              git (
                branch: 'main',
                credentialsId: 'Talits',
                url: 'git@github.com:Talits/ada-ci.git'
              )
            }
        }

        stage('Build') {
            when {
                branch "main"
            } 
            steps { 
                script{
                 image = docker.build("talits/v1:main")
                }
            }
        }
        stage('Build dev'){
            when {
                not {
                    branch 'main'
                }
            }
            steps { 
                script{
                 image = docker.build("talits/v1:develop")
                }
            }
        }
        stage('Push') {
            steps {
                script{
                       docker.withRegistry('', 'docker') {
                       image.push()
                    }
                }
            }
        }
    }
}
