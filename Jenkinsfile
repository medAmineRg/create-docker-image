// pipeline {
//     agent { dockerfile true }
//     stages {
//         stage('Build') {
//             steps {
//                checkout scmGit(branches: [[name: '*/master']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/medAmineRg/create-docker-image']])
//                 sh "npm i"
//             }
//         }
//         stage('Build Image') {
//             steps {
//                 script {
//                     def customImage = docker.build("my-image:${env.BUILD_ID}")
//                 }
//             }
//         }
//         // stage('Push') {
//         //     steps {
//         //         script {
//         //             withCredentials([string(credentialsId: 'dockerhub', variable: 'dockerhub')]) {
//         //                 dockerImage.push()
//         //             }
//         //         }
//         //     }
//         // }
//     }
// }

node {   
    stage('Clone repository') {
        git credentialsId: 'git', url: 'https://github.com/medAmineRg/create-docker-image'
    }

    environment {
        DOCKERHUB_CREDENTIALS = credentials('dockerhubjenkins')
    }
    
    stage('Build image') {
       dockerImage = docker.build("dev/khobz")
    }

    stage('Login') {
      steps {
        sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'
      }
    }
    
     stage('Push image') {
            // withDockerRegistry(credentialsId: 'dockerhubjenkins', url: 'https://hub.docker.com/') {
                dockerImage.push()
        // }
    }    
}

