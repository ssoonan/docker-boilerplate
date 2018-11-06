pipeline {
    agent any
    stages {
        stage('build') {
            steps {
                echo 'build docker image'
                sh '''
                docker build -t zapper0703/python-pipenv:$BUILD_NUMBER-base -f python-pipenv/Dockerfile.base python-pipenv
                '''
            }
        }

        stage('push') {
            steps {
            withDockerRegistry([credentialsId: "ad602a39-f4eb-4fc2-9a25-9c1f531c4702", url: ""]){
            echo 'docker image push'
            sh '''
            docker push zapper0703/python-pipenv:$BUILD_NUMBER-base
            '''
            }
            }

        }
    }
}