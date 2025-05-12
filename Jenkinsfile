pipeline {
    agent any

    environment {
        SONAR_HOST_URL = 'http://localhost:8081'  // adapte si autre IP
    }

    stages {

        stage('Cloner le dépôt') {
            steps {
                git url: 'https://github.com/Aziztn28/spring--boot-ci-cd.git', branch: 'main'
            }
        }

        stage('Compilation Maven') {
            steps {
                sh 'mvn clean install -DskipTests'
            }
        }

        stage('Analyse SonarQube') {
            steps {
                withSonarQubeEnv('sonar-token') {
                    sh 'mvn sonar:sonar -Dsonar.projectKey=springboot-ci -Dsonar.host.url=$SONAR_HOST_URL -Dsonar.login=${SONAR_AUTH_TOKEN}'
                }
            }
        }

        stage('Docker Build') {
            steps {
                sh 'docker build -t springboot-ci-app:latest .'
            }
        }
    }

    post {
        success {
            echo '✅ Pipeline exécuté avec succès !'
        }
        failure {
            echo '❌ Échec du pipeline.'
        }
    }
}
