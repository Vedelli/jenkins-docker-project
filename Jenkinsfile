pipeline {
    agent any

    stages {
        stage('Clone Repo') {
            steps {
                git branch: 'main',
                    url: 'https://github.com/Vedelli/jenkins-docker-project.git',
                    credentialsId: 'github-pat'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t jenkins-docker-project-app .'
            }
        }

        stage('Run Docker Container') {
            steps {
                sh '''
                # Stop old container if exists
                docker stop jenkins-docker-project-app || true
                docker rm jenkins-docker-project-app || true

                # Run new container
                docker run -d -p 80:5000 --name jenkins-docker-project-app jenkins-docker-project-app
                '''
            }
        }
    }
}