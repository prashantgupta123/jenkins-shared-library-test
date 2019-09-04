#!groovy

pipeline {
    agent any
    environment {
        CC = 'clang'
        GITHUB = credentials('Git-Hub')
    }
    stages {
        stage('Build') {
            steps {
                echo "Hello world!"
            }
        }
        stage('Environment') {
            steps {
                sh 'echo "GITHUB user is $GITHUB_USR"'
                sh 'echo "GITHUB password is $GITHUB_PSW"'
            }
        }
    }
    post {
        always {
            echo 'I will always say Hello again!'
        }
    }
}