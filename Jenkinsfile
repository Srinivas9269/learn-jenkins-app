pipeline {
    agent any

    stages {
        stage('Build') {
            agent {
                docker {
                    image 'node:18-alpine'
                    reuseNode true
                }
            }
            steps {
                sh '''
                    # Install dependencies needed to build native modules
                    apk add --no-cache python3 make g++ bash

                    # Clean previous build
                    rm -rf node_modules .npm-cache

                    # Use workspace-local npm cache (avoids permissions issues)
                    mkdir -p $WORKSPACE/.npm-cache

                    # Show versions and info
                    node --version
                    npm --version
                    npm config set cache $WORKSPACE/.npm-cache

                    # Install dependencies and build
                    npm ci
                    npm run build

                    # List files after build
                    ls -la
                '''
            }
        }
    }
}
