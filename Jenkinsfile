pipeline {
    agent { 
        label 'wsl'
    }
    stages {
        stage('Build de la aplicación') {
            steps {
                sh 'docker build -t webserver .'
            }
        }
        stage('Publicar imagen de la aplicación') {
            steps {
                script {
                    docker.withRegistry("https://ghcr.io", "reg-cred-id") {
                        sh "docker tag hello-world ghcr.io/sebastianxjavier/hello-world:${env.BUILD_NUMBER}"
                        sh "docker push ghcr.io/sebastianxjavier/hello-world:${env.BUILD_NUMBER}"
                        sh 'docker tag hello-world ghcr.io/sebastianxjavier/hello-world:latest'
                        sh 'docker push ghcr.io/sebastianxjavier/hello-world:latest'
                    }
                }
            }
        }
        stage('Deploy de la aplicación') {
            steps {
                sh "kubectl set image deployment/hello-world hello-world=ghcr.io/sebastianxjavier/hello-world:${env.BUILD_NUMBER}"
            }
        }
    }
}