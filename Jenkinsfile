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
                '''
            }
        }
        
        stage('Test'){
            steps{
                echo 'Test stage'
                sh 'test -f build/index.html'
            }

        }
    }
}
