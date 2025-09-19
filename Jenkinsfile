pipeline {
    agent { 
        // docker {
        //     image 'node:24-alpine'
        //     label 'wsl'
        // }
        label 'wsl'
    }
    stages {
        stage('Build de la aplicación') {
            steps {
                sh 'docker build -t webserver .'
            }
        }
    }
}