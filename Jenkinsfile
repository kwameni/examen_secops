pipeline {
    agent any

    tools {
        maven 'MAVEN_HOME'  // Nom donné à Maven dans Jenkins (à configurer dans Jenkins > Global Tool Configuration)
    }

    stages {
        stage('Checkout') {
            steps {
                git 'https://github.com/ton-utilisateur/ton-repo.git'
            }
        }

        stage('Build') {
            steps {
                sh 'mvn clean install'
            }
        }

        stage('Test') {
            steps {
                sh 'mvn test'
            }
        }

        stage('Package') {
            steps {
                sh 'mvn package'
            }
        }

        stage('Deploy to Nexus') {
            steps {
                // uniquement si tu veux pousser sur Nexus (et que tu as défini distributionManagement)
                sh 'mvn deploy'
            }
        }
    }

    post {
        success {
            echo 'Pipeline exécuté avec succès.'
        }
        failure {
            echo 'Échec du pipeline.'
        }
    }
}
