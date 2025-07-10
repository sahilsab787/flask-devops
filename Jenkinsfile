pipeline {
    agent any

    stages {
        stage('Clone') {
            steps {
                git branch: 'main',
                    credentialsId: 'github-creds',
                    url: 'https://github.com/sahilsab787/flask-devops.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    sh 'docker build -t flask-devops-app .'
                }
            }
        }

        stage('Stop Old Container') {
            steps {
                script {
                    // Agar pehle se chal raha ho to stop & remove
                    sh '''
                    docker stop flask-app || true
                    docker rm flask-app || true
                    '''
                }
            }
        }

        stage('Run Docker Container') {
            steps {
                script {
                    sh 'docker run -d -p 5000:5000 --name flask-app flask-devops-app'
                }
            }
        }
    }
}
