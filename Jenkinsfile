@Library('jenkins-demo-lib') _

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
        stage('Say Hello') {
            sayHello
        }
        stage('Set Version') {
            steps {
                script {
                    def date = new Date()
                    print date
                }
                sh 'gradle clean build -x test'
            }
        }
        stage('Build') {
            steps {
                sh 'gradle clean build -x test'
            }
        }
        stage('Test') {
            steps {
                sh 'gradle cleanTest test'
            }
        }
        stage('Archive') {
            steps {
                sh 'gradle publish'
            }
        }
    }
    post {
        success {
            archiveArtifacts artifacts: 'build/libs/**/*.jar', fingerprint: true
        }
        always {
            junit 'build/test-results/**/*.xml'
        }
    }
}