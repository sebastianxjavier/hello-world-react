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
  -  name: kubectl
     image: alpine/k8s:1.32.2
     command: ["/bin/sh", "-c", "tail -f /dev/null"]
  -  name: kaniko
     image: gcr.io/kaniko-project/executor:debug
     command: ["/bin/sh", "-c", "tail -f /dev/null"]
            """
        }
    }
    stages {
        stage('Build de la imagen') {
            steps {
                container('kaniko') {
                    sh 'ls -la /kaniko/.docker'
                    sh 'cat /kaniko/.docker/.config.json'
                }
            }
        }
        // stage('kubectl para cluster') {
        //     steps {
        //         container('kubectl') {
        //             sh 'kubectl get pod'
        //         }
        //     }
        // }
    }
}