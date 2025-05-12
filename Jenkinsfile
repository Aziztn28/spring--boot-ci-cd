<<<<<<< HEAD
pipeline {
    agent any  // Cela signifie que Jenkins peut exécuter ce pipeline sur n'importe quel agent disponible

    environment {
        // URL et token pour SonarQube
        SONAR_HOST_URL = 'http://localhost:8081'  // Remplacez par l'URL de votre serveur SonarQube
        SONAR_AUTH_TOKEN = credentials('sonar_token')  // Remplacez 'sonar_token' par l'ID de votre token stocké dans Jenkins
    }

    stages {
        // Étape 1 : Cloner le projet depuis GitHub
        stage('Cloner le projet') {
            steps {
                git url: 'https://github.com/Aziztn28/spring--boot-ci-cd.git', branch: 'main'  // Remplacez par l'URL de votre repository GitHub
            }
        }

        // Étape 2 : Compiler le projet avec Maven
        stage('Build Maven') {
            steps {
                sh 'mvn clean install -DskipTests'  // Utilisation de Maven pour compiler et créer l'artefact, tests sont ignorés
            }
        }

        // Étape 3 : Analyser le code avec SonarQube
        stage('Analyse SonarQube') {
            steps {
                withSonarQubeEnv('SonarQube') {  // Assurez-vous que SonarQube est configuré dans Jenkins sous "Manage Jenkins" -> "Configure System"
                    sh 'mvn sonar:sonar -Dsonar.projectKey=springboot-ci-cd -Dsonar.host.url=${env.SONAR_HOST_URL} -Dsonar.login=${env.SONAR_AUTH_TOKEN}'  // Analyse SonarQube
                }
            }
        }

        // Étape 4 : Construire l'image Docker
        stage('Docker Build') {
            steps {
                sh 'docker build -t springboot-ci-cd:latest .'  // Crée l'image Docker avec le tag "springboot-ci-cd:latest"
            }
        }
    }

    post {
        success {
            echo 'Le pipeline a été exécuté avec succès !'
        }
        failure {
            echo 'Le pipeline a échoué. Veuillez vérifier les logs pour plus de détails.'
        }
    }
}
=======
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
>>>>>>> fe3dd5f5dbbeee22e74f1068d5492a9785f03f80
pipeline {
    agent any

    environment {
        SONAR_HOST_URL = 'http://localhost:9000' // mettez l'IP ou domaine Sonar si différent
        SONAR_TOKEN = credentials('sonar-token') // à configurer dans Jenkins > Credentials
    }

    stages {
        stage('Cloner le dépôt') {
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
                    sh 'mvn sonar:sonar -Dsonar.projectKey=springboot-project -Dsonar.host.url=$SONAR_HOST_URL -Dsonar.login=$SONAR_TOKEN'
                }
            }
        }

        stage('Docker Build') {
            steps {
                sh 'docker build -t springboot-app:latest .'
            }
        }
    }

    post {
        success {
            echo 'Pipeline exécuté avec succès 🎉'
        }
        failure {
            echo 'Erreur dans le pipeline ❌'
        }
    }
}
