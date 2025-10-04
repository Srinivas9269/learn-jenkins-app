pipeline {
    agent any

    stages {
        stage('Build') {
            agent{
                docker{
                    image 'node:18-alpine'
                    reuseNode true
                }
            }
            steps {
                sh '''
                    ls -la
                    node --version
                    npm --version
                    rm -rf node_modules .npm-cache
                    npm ci --cache $(pwd)/.npm-cache
                    npm run build --cache $(pwd)/.npm-cache
                    npm ci
                    npm run build
                    ls -la
                '''
            }
        }
    }
}