#!/usr/bin/env groovy

pipeline {
    agent any

    environment {
        // Set NODE_HOME only if needed. Optional.
        PATH = "/usr/local/bin:$PATH"
    }

    stages {
        stage('Build') {
            steps {
                echo 'Starting Build...'
                sh 'node --version'
                sh 'npm install'
                sh 'npx gulp lint'  // Use npx if gulp is in node_modules
            }
        }

        stage('Test') {
            steps {
                echo 'Starting Test...'
                sh 'node --version'
                sh 'npx gulp test'  // Use npx if gulp is not globally installed
            }
        }
    }

    post {
        always {
            echo 'One way or another, I have finished'
            deleteDir() // clean up workspace
        }
        success {
            echo 'I succeeded!'
        }
        unstable {
            echo 'I am unstable :/'
        }
        failure {
            echo 'I failed :('
        }
        changed {
            echo 'Things were different before...'
        }
    }
}
