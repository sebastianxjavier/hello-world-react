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
     volumeMounts:
	 - name: kaniko-secret
	   mountPath: /kaniko/.docker/config.json
	   subPath: .dockerconfigjson
  volumes:
  -  name: kaniko-secret
     secret:
       secretName: ghcr-registry
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
		// 	steps {
		// 		script {
		// 			container('kubectl') {
		// 				sh "kubectl set image -n curso-contenedores deployment/hello-world hello-world=ghcr.io/sebastianxjavier/hello-world:${env.BUILD_NUMBER}"
		// 			}
		// 		}
		// 	}
		// }
    }
}