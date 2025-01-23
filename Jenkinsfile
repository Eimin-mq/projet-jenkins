pipeline {
    agent any

    environment {
        SONAR_TOKEN = credentials('sonar-token-id')
        MAVEN_HOME = tool name: 'Maven', type: 'ToolLocation'
    }

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }
        stage('Build') {
            steps {
                script {
                         sh "${MAVEN_HOME}/bin/mvn clean install"
                }
            }
        }
        stage('SonarQube Analysis') {
            steps {
                withSonarQubeEnv('SOnarQube') {
                    sh """
                        ${MAVEN_HOME}/bin/mvn sonar:sonar \
                        -Dsonar.projectKey=sqa_2160fc6fd0016fdb3e0047d8095144b22ab8cd62 \
                        -Dsonar.host.url=http://localhost:9000 \
                        -Dsonar.login=${sonar-token-id}
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
        
