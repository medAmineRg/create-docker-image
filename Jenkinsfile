pipeline {
    agent { dockerfile true }
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

