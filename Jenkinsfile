CRON_SETTINGS = '*/5 * * * *'

pipeline {
    agent any
    triggers {
        cron(CRON_SETTINGS)
    }
    stages {
        stage('Checkout') {
            steps {
                git 'https://github.com/atothhpe/jenkins-demo'
            }
        }
        stage('Build') {
            steps {
                sh 'gradle clean build -x'
            }
        }
        stage('Test') {
            steps {
                sh 'gradle clean test'
            }
        }
        stage('Archive') {
            steps {
                echo 'Deploying....'
            }
        }
    }
}