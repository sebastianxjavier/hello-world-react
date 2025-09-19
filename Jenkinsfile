pipeline {
    agent { 
        docker {
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