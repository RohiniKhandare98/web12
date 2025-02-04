pipeline {
    agent any
    environment {
        DOCKER_IMAGE = "rohini1/web_new"
    }

    stages {

        stage('SCM') {
            steps {
                git branch: 'main', url: 'https://github.com/RohiniKhandare98/web12.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh "/usr/bin/docker image build -t ${DOCKER_IMAGE} ."
            }
        }

        stage("Push Docker Image") {
            steps {
                withCredentials([string(credentialsId: 'DOCKER_HUB_TOKEN', variable: 'DOCKER_HUB_TOKEN')]) {
                    sh "echo $DOCKER_HUB_TOKEN | /usr/bin/docker login -u rohini1 --password-stdin"
                    sh "/usr/bin/docker image push ${DOCKER_IMAGE}"
                }
            }
        }

        stage("Deploy Docker Service") {
            steps {
               sh "/usr/bin/docker service rm -rf backend || true"
                sh "/usr/bin/docker run -d --name backend -p 4000:80 ${DOCKER_IMAGE}"
            }
        }
        
    }
}
