pipeline {
    agent any

    tools {
        nodejs 'node-18'  // Make sure you’ve installed this NodeJS version in Jenkins tools
    }

    stages {
        stage('Checkout Code') {
            steps {
                git 'https://github.com/Aarav2411/jenkins-pipeline-example.git'
            }
        }

        stage('Install Dependencies') {
            steps {
                sh 'npm install'
            }
        }

        stage('Run App') {
            steps {
                sh 'node app.js'
            }
        }
    }
}
