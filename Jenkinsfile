pipeline {
    agent {
        docker { image 'node:16-alpine' }
    }
    stages {
        
        stage('Initialize'){
            steps {
                script {
                    def dockerHome = tool 'docker'
                    env.PATH = "${dockerHome}/bin:${env.PATH}"
                }
            }
        }
        stage('Build') {
            steps {
               checkout scmGit(branches: [[name: '*/master']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/medAmineRg/create-docker-image']])
                sh "npm i"
            }
        }

        stage('Build Image') {
            steps {
                script {
                    sh 'docker build image -t devops/real-project .'
                }
            }
        }

        stage('Push') {
            steps {
                script {
                    withCredentials([string(credentialsId: 'dockerhub', variable: 'dockerhub')]) {
                        sh 'docker login -u mohamed99amine -p ${dockerhub}'
                        sh 'docker push devops/real-project'
                    }
                }
            }
        }
    }
}

