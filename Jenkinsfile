pipeline {
    agent any

    tools {
        maven 'maven3' // Assurez-vous que 'maven3' correspond au nom de votre installation Maven dans Jenkins
        jdk 'jdk-21'   // Assurez-vous que vous avez bien configuré JDK 21 dans Jenkins
    }

    environment {
        SONARQUBE_TOKEN = 'sqp_12d5514c18a0c857383266dd66268233f66e8ad6'  // Votre token SonarQube
        SONARQUBE_URL = 'http://localhost:9000'  // URL de votre serveur SonarQube
    }

    stages {
        stage('Checkout') {
            steps {
                checkout scm  // Récupère le code source de votre dépôt GitHub
            }
        }

        stage('Build and SonarQube Analysis') {
            steps {
                script {
                    // Exécution de Maven avec SonarQube
                    sh '''mvn clean verify sonar:sonar \
                    -Dsonar.projectKey=github-projet-jenkins \
                    -Dsonar.projectName="SonJenHub" \
                    -Dsonar.host.url=$SONARQUBE_URL \
                    -Dsonar.token=$SONARQUBE_TOKEN'''
                }
            }
        }
    }

    post {
        always {
            // Actions à réaliser après le pipeline (notifications, nettoyage, etc.)
        }
    }
}
