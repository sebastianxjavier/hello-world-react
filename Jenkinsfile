pipeline {
    agent { 
        kubernetes {
            yaml """
apiVersion: v1
kind: Pod
spec:
  serviceAccountName: jenkins-account
  containers:
  -  name: node
     image: node:24-alpine
     command: ["/bin/sh", "-c", "tail -f /dev/null"]
            """
        }
    }
    stages {
        stage('Build de la aplicación') {
            steps {
                container('node') {
                    sh 'node --version'
                }
            }
        }
    }
}