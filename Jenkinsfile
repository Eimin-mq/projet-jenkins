pipeline {
    agent any

    environment {
        // Définir le token SonarQube dans les variables d'environnement
        SONAR_TOKEN = 'sqp_12d5514c18a0c857383266dd66268233f66e8ad6' // Remplacer si nécessaire
    }

    stages {
        stage('Checkout') {
            steps {
                // Récupérer le code du dépôt Git
                checkout scm
            }
        }

        stage('Build & Verify') {
            steps {
                // Exécuter Maven3 pour nettoyer, vérifier et analyser avec SonarQube
                script {
                    sh """
                        maven3 clean verify sonar:sonar \
                            -Dsonar.projectKey=github-projet-jenkins \
                            -Dsonar.projectName='SonJenHub' \
                            -Dsonar.host.url=http://localhost:9000 \
                            -Dsonar.token=${SONAR_TOKEN}
                    """
                }
            }
        }
    }

    post {
        success {
            echo "Pipeline terminé avec succès"
        }
        failure {
            echo "Pipeline échoué"
        }
    }
}
