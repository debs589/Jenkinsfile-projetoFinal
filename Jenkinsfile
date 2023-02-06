pipeline {
    agent {label 'worker'}
    stages {
        stage('Clone repository') { 
            steps {
              git (
                branch: 'main',
                credentialsId: 'af164527-d6d2-4e6b-b7ae-47c54f22637b',
                url: 'git@github.com:debs589/ada-ci.git'
              )
            }
        }

        
        stage('Build dev'){
            when {
               not {
                  branch "main"
               }
            }
            steps { 
                script{
                 image = docker.build("debs589/v1:develop")
                 
                }
            }
        }
        stage('Build') {
            when {
                branch "main"
            } 
            steps { 
                script{
                 image = docker.build("debs589/v1:main")
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
