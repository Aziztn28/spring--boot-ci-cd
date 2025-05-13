pipeline {
    agent any

    tools {
        maven 'Maven 3.8.6'   // Corrigé ici
        jdk 'JDK 21'          // Assure-toi que ce nom existe aussi dans Jenkins
    }

    environment {
        MAVEN_HOME = tool 'Maven 3.8.6'
        JAVA_HOME = tool 'JDK 21'
        PATH = "${JAVA_HOME}/bin:${MAVEN_HOME}/bin:${env.PATH}"
    }

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main',
                    url: 'https://github.com/Aziztn28/spring--boot-ci-cd pipeline.git'
            }
        }

        stage('Build') {
            steps {
                bat 'mvn clean compile'
            }
        }

        stage('Test') {
            steps {
                bat 'mvn test'
            }
        }

        stage('Package') {
            steps {
                bat 'mvn package'
            }
        }
    }

    stage('SonarQube Analysis') {
    steps {
        withSonarQubeEnv('SonarQube') {
            sh 'mvn sonar:sonar \
                -Dsonar.projectKey=springboot-ci-cd-pipeline \
                -Dsonar.host.url=http://localhost:8001 \
                -Dsonar.login=<TON_TOKEN>'
        }
    }
}


    post {
        success {
            echo '✅ Build réussi !'
        }
        failure {
            echo '❌ Le build a échoué.'
        }
    }
}