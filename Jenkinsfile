
stage('Build') {
  agent {
    docker {
      image 'node:18-bullseye'
      args '-u root'     // run as root to avoid permission bugs
      reuseNode true
    }
  }
  steps {
    sh '''
    
      set -e

      # Fix permissions
      chown -R node:node .

      # Upgrade npm (fixes the "Exit handler never called!" bug)
      npm install -g npm@latest

      # Install deps as root (works fine in CI)
      npm ci

      # Build
      npm run build
      ls -la
    '''
  }
}

