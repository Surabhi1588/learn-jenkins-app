pipeline {
    agent any

    stages {
        stage('Build') {
            agent{
                docker{
                    image 'node:18-bullseye'    // or node:20-bullseye if compatible
                    args '-u 0:0'               // run container as root to fix perm
                    reuseNode true
                }
            }
            steps {
                sh'''
                    ls -la
                    node --version
                    npm --version
                    npm install -g npm@latest
                    npm ci
                    npm run build
                    ls -la
                '''
            }
        }
    }
}
