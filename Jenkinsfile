pipeline {
    agent any

    stages {
        stage('Clone repository') {
            steps {
                checkout scm
            }
        }

        stage('Build image') {
            when {
                branch 'develop'
            }
            steps {
                script {
                    app = docker.build("nnikolovskii/kiii_domasno_3")
                }
            }
        }

        stage('Push image') {
            when {
                branch 'develop'
            }
            steps {
                script {
                    docker.withRegistry('https://registry.hub.docker.com', 'dockerhub') {
                        app.push("${env.BRANCH_NAME}-${env.BUILD_NUMBER}")
                        app.push("${env.BRANCH_NAME}-latest")
                    }
                }
            }
        }
    }
}
