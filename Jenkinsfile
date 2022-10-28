pipeline {
    agent { label 'tuto' }

    environment{
        DOCKERHUB_CREDS = credentials("jenkins-id")
    } 

    stages {
        stage('Build') {
            steps {
                container('podman') {
                    script {
                        sh 'podman build -t docker.io/edgardog/web-go:$BUILD_NUMBER -f Dockerfile'
                        sh 'podman login docker.io -u $DOCKERHUB_CREDS_USR -p $DOCKERHUB_CREDS_PW'
                        sh 'podman oush docker.io/edgardog/web-go:$BUILD_NUMBER'
                    }
                }
                container('kubectl') {
                    script {
                        sh 'podman build'
                    }
                } 
            }
        }
    }
}