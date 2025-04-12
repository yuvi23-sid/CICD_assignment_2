pipeline {
  agent any

  environment {
    NETLIFY_SITE_ID = credentials('NETLIFY_SITE_ID')
    NETLIFY_AUTH_TOKEN = credentials('NETLIFY_AUTH_TOKEN')
  }

  stages {
    stage('Build') {
      steps {
        bat 'npm install'
      }
    }

    stage('Test') {
      steps {
        bat 'npm test -- --watchAll=false --passWithNoTests'
      }
    }

    stage('Deploy') {
      steps {
        bat 'npm install -g netlify-cli'
        bat 'npm run build'
        bat 'netlify deploy --prod --dir=build --site=$NETLIFY_SITE_ID --auth=$NETLIFY_AUTH_TOKEN'
      }
    }
  }
}
