// pipeline {
//     agent {
//         docker { image 'node:16-alpine' }
//     }
//     stages {
        
//         stage('Initialize'){
//             steps {
//                 script {
//                     def dockerHome = tool 'docker'
//                     env.PATH = "${dockerHome}/bin:${env.PATH}"
//                 }
//             }
//         }
//         stage('Build') {
//             steps {
//                checkout scmGit(branches: [[name: '*/master']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/medAmineRg/create-docker-image']])
//                 sh "npm i"
//             }
//         }

//         stage('Build Image') {
//             steps {
//                 script {
//                     sh 'docker build image -t devops/real-project .'
//                 }
//             }
//         }
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
                sh 'npm install'
            }
        }
        stage('Test') {
            steps {
                sh './jenkins/scripts/test.sh'
            }
        }
        stage('Deliver') { 
            steps {
                sh './jenkins/scripts/deliver.sh' 
                input message: 'Finished using the web site? (Click "Proceed" to continue)' 
                sh './jenkins/scripts/kill.sh' 
            }
        }
    }
}

//         stage('Push') {
//             steps {
//                 script {
//                     withCredentials([string(credentialsId: 'dockerhub', variable: 'dockerhub')]) {
//                         sh 'docker login -u mohamed99amine -p ${dockerhub}'
//                         sh 'docker push devops/real-project'
//                     }
//                 }
//             }
//         }
//     }
// }

