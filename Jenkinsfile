pipeline {
    agent any
    stages {
        stage('Clone Code') {
            steps {
                git branch: 'master',
                    url: 'https://github.com/iomrarshad/two-tier-flask-app.git'
            }
        }
        stage('Build Docker Image') {
            steps {
                sh 'docker build -t flask-app:latest .'
            }
        }
        stage('Stop Old Container') {
            steps {
                sh 'docker rm -f mysql flask-app || true'
                sh 'docker network rm two-tier-flask-app_twotier || true'
            }
        }
        stage('Deploy App') {
            steps {
                sh 'docker-compose up -d'
            }
        }
    }
    post {
        success {
            echo 'App successfully deployed!'
        }
        failure {
            echo 'Pipeline failed — check logs!'
        }
    }
}
