pipeline {
    agent any
    stages {
        stage('Test') {
            agent {
                docker { image 'node:18.17.1-alpine3.18' }
            }
            steps {
                sh 'node --version'
            }
        }
    }
}