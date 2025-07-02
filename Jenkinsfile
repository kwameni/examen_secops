pipeline {
    agent any

    tools {
        maven 'MAVEN_HOME' // À configurer dans Jenkins : Global Tool Configuration
    }

    environment {
        MAVEN_OPTS = '-Dmaven.test.failure.ignore=true'
    }

    stages {
        stage('Checkout') {
            steps {
                git 'https://github.com/kwameni/examen_secops.git'
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
                withCredentials([usernamePassword(credentialsId: 'nexus-credentials', usernameVariable: 'NEXUS_USER', passwordVariable: 'NEXUS_PASS')]) {
                    sh 'mvn deploy -Dnexus.username=$NEXUS_USER -Dnexus.password=$NEXUS_PASS'
                }
            }
        }
    }

    post {
        success {
            echo '✅ Pipeline exécuté avec succès.'
        }
        failure {
            echo '❌ Échec du pipeline.'
        }
    }
}
