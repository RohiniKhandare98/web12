pipeline {
    agent any

    stages {
        stage('git') {
            steps {
                git 'https://github.com/RohiniKhandare98/CDAC_Project.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    sh 'docker build -t web3 .'
                }
            }
        }

        stage('Run Docker Container') {
            steps {
                script {
                    sh 'docker run -d -p 8000:80 --name myapache-container web3'
                }
            }
        }
    }
}
