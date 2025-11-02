pipeline {
    agent any

    tools {
        maven 'Maven-3.9'   // name from your Jenkins Global Tool Configuration
    }

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Build') {
            steps {
                bat 'mvn -B clean package'
            }
        }

        stage('Archive') {
            steps {
                archiveArtifacts artifacts: 'target/*.jar', fingerprint: true
            }
        }

        stage('Run') {
            steps {
                bat 'java -jar target/hello-jenkins-1.0-SNAPSHOT.jar'
            }
        }
    }

    post {
        success {
            echo '🎉 Build and run successful!'
        }
        failure {
            echo '❌ Build failed — check console output.'
        }
    }
}
