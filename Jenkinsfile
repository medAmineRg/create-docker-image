pipeline {
    agent {
        docker { image 'node:lts-alpine3.18' }
    }
    stages {

        stage('Build') {
            steps {
                sh "node -v"
                sh "npm i"
                sh "ls"
            }
        }

        stage('Test') {
            steps {
                echo 'testing...'
            }
        }

        stage('Deliver') {
            steps {
                echo 'building...'
            }
        }
    }
}