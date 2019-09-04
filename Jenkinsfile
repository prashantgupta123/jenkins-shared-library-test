#!groovy

pipeline {
    agent any
    stages {
        stage('Build') {
            steps {
                echo "Hello world!"
            }
        }
    }
    post {
        always {
            echo 'I will always say Hello again!'
        }
    }
}