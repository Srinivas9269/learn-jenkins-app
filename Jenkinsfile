pipeline {
    agent any

    stages {
        stage('Build') {
            agent {
                docker {
                    image 'node:18-alpine'
                    args '-u root:root'   // run as root to avoid UID mismatch
                    reuseNode true
                }
            }
            steps {
                sh '''
                    # install build dependencies
                    apk add --no-cache python3 make g++ bash

                    # make sure npm cache is inside the workspace
                    mkdir -p $WORKSPACE/.npm-cache
                    mkdir -p $WORKSPACE/.npm-tmp
                    npm config set cache $WORKSPACE/.npm-cache --global
                    npm config set tmp $WORKSPACE/.npm-tmp --global

                    echo "=== Environment Check ==="
                    pwd
                    ls -la
                    node --version
                    npm --version
                    npm config list

                    echo "=== Install & Build ==="
                    npm ci
                    npm run build

                    echo "=== Post Build Files ==="
                    ls -la
                '''
            }
        }
    }
}
