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
                    ls -la
                    node --version
                    npm --version
                    nslookup registry.npmjs.org || true
                    echo "=== RUNNING NPM ===      echo "=== RUNNING NPM ==="
                    npm install -g npm@6
                    npm ci
                    npm run build
                    ls -la
                '''
            }
        }
    }
}
