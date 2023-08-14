pipeline {
    agent {
        docker {
            image 'node:18.17.1-alpine3.18'
            args '-p 3000:3000'
        }
    }
    stage('Initialize'){
             steps {
                script {
                    def dockerHome = tool 'myDocker'
                    env.PATH = "${dockerHome}/bin:${env.PATH}"
                }
             }
    }
    stages {
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

