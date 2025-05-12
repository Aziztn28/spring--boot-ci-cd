pipeline {
    agent any

    environment {
        SONAR_HOST_URL = 'http://localhost:8081'  // adapte si ton SonarQube a une autre IP ou port
    }

    stages {

        stage('Cloner le projet') {
            steps {
                git url: 'https://github.com/Aziztn28/spring--boot-ci-cd.git', branch: 'main'
            }
        }

        stage('Build Maven') {
            steps {
                sh 'mvn clean install -DskipTests'
            }
        }

        stage('Analyse SonarQube') {
            steps {
                withSonarQubeEnv('sonar-token') {
                    sh 'mvn sonar:sonar -Dsonar.projectKey=spring-boot-project -Dsonar.host.url=$SONAR_HOST_URL -Dsonar.login=<TON_TOKEN>'
                }
            }
        }

        stage('Docker Build') {
            steps {
                sh 'docker build -t springboot-ci-cd:latest .'
            }
        }
    }

    post {
        success {
            echo '✅ Pipeline terminé avec succès.'
        }
        failure {
            echo '❌ Échec du pipeline.'
        }
    }
}
