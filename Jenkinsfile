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
        stage('Build image') {
           dockerImage = docker.build("mohamed99amine/devkhobzix")
        }
         stage('Push image') {
            // withDockerRegistry(credentialsId: 'dockerhubjenkins', url: 'https://hub.docker.com/') {
            //     dockerImage.push()
            // }

                withCredentials([string(credentialsId: 'dockerhub', variable: 'dockerhub')]) {
                        sh 'echo ${dockerhub} | docker login -u mohamed99amine --password-stdin'
                }
                sh 'docker push mohamed99amine/devkhobzix'
         }   
}

