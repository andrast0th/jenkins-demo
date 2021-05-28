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
    parameters {
        booleanParam(defaultValue: false, description: 'Publish to Nexus', name: 'SHOULD_PUBLISH')
    }
    stages {
        stage('Checkout') {
            steps {
                git 'https://github.com/atothhpe/jenkins-demo'
            }
        }
        stage('Say Hello') {
            steps {
                sayHello 'Joe'
            }
        }
        stage('Print date') {
            steps {
                script {
                    def date = new Date()
                    print date
                    env.CUSTOM_DATE = date.toString()
                }
                echo "$BRANCH_NAME"
                echo "$BUILD_NUMBER"
                echo "$JOB_NAME"
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
        stage('Publish') {
            when {
                expression { params.SHOULD_PUBLISH }
            }
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