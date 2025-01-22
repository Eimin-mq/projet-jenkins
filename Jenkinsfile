pipeline {
    agent any // Utilise n'importe quel agent Jenkins disponible

    tools {
        maven 'Maven' // Nom de l'installation Maven configurée dans Jenkins
    }

    stages {
        stage("Build") {
            steps {
                echo 'Building the project...'
                // Vérifie la version de Maven installée
                sh 'mvn -v'
                // Compile le projet
                sh 'mvn clean install'
            }
        }

        stage("Test") {
            steps {
                echo 'Running tests...'
                // Exécute les tests unitaires
                sh 'mvn test'
            }
        }

        stage("Deploy") {
            steps {
                echo 'Deploying the application...'
                // Ajouter des étapes spécifiques au déploiement
            }
        }
    }

    post {
        always {
            echo 'Pipeline finished.'
        }
        success {
            echo 'Build succeeded.'
        }
        failure {
            echo 'Build failed.'
        }
    }
}
