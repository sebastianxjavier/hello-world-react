pipeline {
    agent { 
        docker {
            image 'node:24-alpine'
            label 'wsl'
        }
    }
    stages {
        stage('Build de la aplicación') {
            steps {
                sh 'npm install'
            }
        }
    }
}