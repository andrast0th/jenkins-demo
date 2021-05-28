CRON_SETTINGS = '*/5 * * * *'

pipeline {
    agent any
    triggers {
        cron(CRON_SETTINGS)
    }
    tools {
        gradle 'gradle'
    }
    stages {
        stage('Checkout') {
            steps {
                git 'https://github.com/atothhpe/jenkins-demo'
            }
        }
        stage('Build') {
            steps {
                sh 'gradle clean build -x test'
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