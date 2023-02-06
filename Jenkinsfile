pipeline {
    agent {label 'nodoprojeto'}
    stages {
        stage('Clone repository') {
            steps {
              git (
                branch: 'main',
                url: 'git@github.com:vasconsaurus/ada-ci.git'
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
                 image = docker.build("vasconsaurus/v1:develop")
                }
            }
        }
        stage('Build') {
            when {
                branch "main"
            }
            steps {
                script{
                 image = docker.build("vasconsaurus/v1:main")
                }
            }
        }
        stage('Push') {
            steps {
                script{
                       docker.withRegistry('', 'docker-hub') {
                       image.push()
                    }
                }
            }
        }
    }
}
