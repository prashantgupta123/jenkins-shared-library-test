#!groovy

pipeline {
    agent any
    environment {
        CC = 'clang'
        GITHUB = credentials('Git-Hub')
    }
    options {
        skipDefaultCheckout() //Skip checking out code from source control
        disableConcurrentBuilds() //Disallow concurrent executions of the Pipeline
        disableResume() //Do not allow the pipeline to resume if the master restarts
        timeout(time: 1, unit: 'HOURS') //Set a timeout period for the Pipeline run, after which Jenkins should abort the Pipeline
    }
    parameters {
        string(name: 'PERSON', defaultValue: 'Mr Jenkins', description: 'Who should I say hello to?')

        text(name: 'BIOGRAPHY', defaultValue: '', description: 'Enter some information about the person')

        booleanParam(name: 'TOGGLE', defaultValue: true, description: 'Toggle this value')

        choice(name: 'CHOICE', choices: ['One', 'Two', 'Three'], description: 'Pick something')

        password(name: 'PASSWORD', defaultValue: 'SECRET', description: 'Enter a password')
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
        stage('Parameters') {
            steps {
                echo "Hello ${params.PERSON}"

                echo "Biography: ${params.BIOGRAPHY}"

                echo "Toggle: ${params.TOGGLE}"

                echo "Choice: ${params.CHOICE}"

                echo "Password: ${params.PASSWORD}"
            }
        }
        stage('Input') {
            input {
                message "Should we continue?"
                ok "Yes, we should."
                submitter "alice,bob"
                parameters {
                    string(name: 'PERSON', defaultValue: 'Mr Jenkins', description: 'Who should I say hello to?')
                }
            }
            steps {
                echo "Hello, ${PERSON}, nice to meet you."
            }
        }
        stage('Deploy') {
            when {
                branch 'master'
                environment name: 'DEPLOY_TO', value: 'production'
            }
            steps {
                echo 'Deploying'
            }
        }
    }
    post {
        always {
            echo 'I will always say Hello again!'
        }
    }
}