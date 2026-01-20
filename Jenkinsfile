pipeline {
    agent any

    stages {
        stage('Build') {
            agent{
                docker{
                    image 'node:18'    // or node:20-bullseye if compatible
                    args '--dns=8.8.8.8 --dns=1.1.1.1'
                    reuseNode true
                }
            }
            steps {
                sh'''
                    set -e
                    ls -la
                    node --version
                    npm --version
                    echo "=== Test DNS via ping ==="
                    ping -c 1 registry.npmjs.org || true
                    echo "=== Test DNS via curl ==="
                    curl -I https://registry.npmjs.org || true
                    npm install -g npm@latest
                    npm ci
                    npm run build
                    ls -la
                '''
            }
        }
    }
}
