pipeline {
    agent any

    tools {
        maven 'Maven'
        jdk 'JDK'
    }

    stages {

        stage('Checkout') {
            steps {
                git 'https://github.com/milieu0/Teedy.git'
            }
        }

        stage('Build') {
            steps {
                sh 'mvn clean compile'
            }
        }

        stage('PMD Check') {
            steps {
                sh 'mvn pmd:pmd'
            }
        }

        stage('Test') {
            steps {
                sh 'mvn test'
            }
        }

        stage('Generate Test Report') {
            steps {
                sh 'mvn surefire-report:report'
            }
        }

        stage('Generate JavaDoc') {
            steps {
                sh 'mvn javadoc:javadoc'
            }
        }

        stage('Package') {
            steps {
                sh 'mvn package'
            }
        }
    }

    post {
        always {
            archiveArtifacts artifacts: '**/target/*.jar', fingerprint: true
            archiveArtifacts artifacts: '**/site/**/*.*', fingerprint: true
        }
    }
}