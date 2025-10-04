pipeline {
    agent any

    stages {
        stage('Build') {
            agent {
                docker {
                    image 'node:18-alpine'
                    args '-u root:root'
                    reuseNode true
                }
            }
            steps {
                sh '''
                    apk add --no-cache python3 make g++ bash
                    rm -rf node_modules .npm-cache
                    mkdir -p $WORKSPACE/.npm-cache
                    node --version
                    npm --version
                    npm config set cache $WORKSPACE/.npm-cache
                    npm ci
                    npm run build
                    ls -la
                '''
            }
        }
    }
}
