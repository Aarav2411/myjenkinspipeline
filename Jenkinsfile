pipeline {
    agent any

    stages {
        stage('Setup Node.js') {
            steps {
                sh '''
                    echo "Installing NVM and Node.js"
                    export NVM_DIR="$WORKSPACE/.nvm"
                    mkdir -p "$NVM_DIR"  # ✅ FIX: Ensure directory exists
                    curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.7/install.sh | bash
                    [ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh"
                    nvm install 14
                    nvm use 14
                    node -v
                    npm -v
                '''
            }
        }

        stage('Build') {
            steps {
                sh 'npm install'
            }
        }

        stage('Test') {
            steps {
                sh 'npm test'
            }
        }
    }

    post {
        always {
            echo 'Cleaning up workspace...'
            deleteDir()
        }
        failure {
            echo '❌ Build failed!'
        }
        success {
            echo '✅ Build succeeded!'
        }
    }
}
