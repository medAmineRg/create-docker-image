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
           dockerImage = docker.build("dev/khobz")
        }
         stage('Push image') {
            // withDockerRegistry(credentialsId: 'dockerhubjenkins', url: 'https://hub.docker.com/') {
            //     dockerImage.push()
            // }

                 withCredentials([string(credentialsId: 'dockerhub', variable: 'dockerhub')]) {
                   sh 'docker login -u mohamed99amine -p ${dockerhubpwd}'

}
                   sh 'docker push dev/khobz'
         }   
}

