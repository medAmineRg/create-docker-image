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
                    def customImage = docker.build("my-image:${env.BUILD_ID}")
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

