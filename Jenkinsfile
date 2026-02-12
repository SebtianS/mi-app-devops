pipeline {
    agent any

    stages {
        stage('Build Docker Image') {
            steps {
                sh 'docker build -t mi-app .'
            }
        }

        stage('Approval Required') {
            steps {
                input message: '¿Aprobar despliegue a producción?', ok: 'Aprobar'
            }
        }

        stage('Stop Old Container') {
            steps {
                sh 'docker rm -f mi-app-container || true'
            }
        }

        stage('Run New Container') {
            steps {
                sh 'docker run -d -p 3000:3000 --name mi-app-container mi-app'
            }
        }
    }
}