pipeline {
    agent any
    
    environment {
        SONAR_TOKEN = credentials('sonar-token-id')
    }

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }
        stage('Build') {
            steps {
                sh 'mvn clean install'
            }
        }
        stage('SonarQube Analysis') {
            steps {
                withSonarQubeEnv('SonJenHub') {
                    sh """
                        mvn sonar:sonar \
                        -Dsonar.projectKey=sqa_2160fc6fd0016fdb3e0047d8095144b22ab8cd62 \
                        -Dsonar.host.url=http://localhost:9000 \
                        -Dsonar.login=${SONAR_TOKEN}
                    """
                }
            }
        }
    }

    post {
        success {
            echo 'Pipeline terminé avec succès !'
        }
        failure {
            echo 'Échec du pipeline.'
        }
    }
}
