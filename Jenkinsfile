pipeline {
    agent {
        docker {
            image 'node:18.17.1-alpine3.18'
            args '-p 3000:3000'
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
                    dockerImage = docker.build("dev/khobz")
                }
            }
        }
        // stage('Push') {
        //     steps {
        //         script {
        //             withCredentials([string(credentialsId: 'dockerhub', variable: 'dockerhub')]) {
        //                 dockerImage.push()
        //             }
        //         }
        //     }
        // }
    }
}

