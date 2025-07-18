pipeline {
    agent any
    environment {
        NODE_VERSION = "10.24.1"
        NVM_DIR = "${WORKSPACE}/.nvm"
    }
    stages {
        stage('Setup Node.js') {
            steps {
                sh '''
                    echo "Installing NVM and Node.js"
                    curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.7/install.sh | bash
                    export NVM_DIR="${NVM_DIR}"
                    [ -s "$NVM_DIR/nvm.sh" ] && . "$NVM_DIR/nvm.sh"
                    nvm install $NODE_VERSION
                    nvm use $NODE_VERSION
                    node -v
                    npm -v
                '''
            }
        }

        stage('Build') {
            steps {
                sh '''
                    export NVM_DIR="${NVM_DIR}"
                    [ -s "$NVM_DIR/nvm.sh" ] && . "$NVM_DIR/nvm.sh"
                    nvm use $NODE_VERSION
                    npm install
                    gulp lint
                '''
            }
        }

        stage('Test') {
            steps {
                sh '''
                    export NVM_DIR="${NVM_DIR}"
                    [ -s "$NVM_DIR/nvm.sh" ] && . "$NVM_DIR/nvm.sh"
                    nvm use $NODE_VERSION
                    gulp test
                '''
            }
        }
    }

    post {
        always {
            echo 'Cleaning up workspace...'
            deleteDir()
        }
        success {
            echo '✅ Build succeeded!'
        }
        failure {
            echo '❌ Build failed!'
        }
    }
}
