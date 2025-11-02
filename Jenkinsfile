pipeline {
    agent any
    tools { maven 'Maven-3.9' }
    stages {
        stage('Checkout') {
            steps { checkout scm }
        }
        stage('Build') {
            steps {
                dir('my-app') {   // 👈 go into subfolder
                    bat 'mvn -B clean package'
                }
            }
        }
        stage('Test') {
            steps {
                dir('my-app') {
                    bat 'mvn test'
                }
            }
            post {
                always {
                    junit 'my-app/target/surefire-reports/*.xml'
                }
            }
        }
        stage('Archive') {
            steps {
                archiveArtifacts artifacts: 'my-app/target/*.jar', fingerprint: true
            }
        }
    }
}
