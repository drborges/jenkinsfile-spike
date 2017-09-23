pipeline {
  agent any
  stages {
    stage('Checkout') {
      steps {
        echo 'checking out git revision...'
        echo 'initing ruby env...'
        echo 'placing configs...'
      }
    }
    stage('Install') {
      steps {
        parallel (
          bundle: { echo 'running bundle install...' },
          yarn: { echo 'warm yarn cache + install...' },
        )
      }
    }
    stage('Integrity Checks') {
      steps {
        echo 'looking for unexpected yarn.lock changes...'
        echo 'looking for unexpected structure.sql changes...'
        echo 'looking for unexpected file changes...'
      }
    }
    stage('Build') {
      steps {
        parallel(
          transition: { echo 'building...' },
          comp1: { echo 'building...' },
          comp2: { echo 'building...' },
          comp3: { echo 'building...' },
          comp4: { echo 'building...' },
          comp5: { echo 'building...' },
          umbrella: { echo 'building...' },
        )
      }
    }
    stage('Lint + Test') {
      steps {
        parallel(
          transition: { echo 'testing...' },
          comp1: { echo 'testing...' },
          comp2: { echo 'testing...' },
          comp3: { echo 'testing...' },
          comp4: { echo 'testing...' },
          comp5: { echo 'testing...' },
          umbrella: { echo 'testing...' },
        )
      }
    }
    stage('Artifacts') {
      steps {
        parallel(
          client: { echo 'generating webpack bundle...' },
          generator: { echo 'component generator checks...' },
          docs: { echo 'generating ruby docs...' },
        )
      }
    }
    stage('QA Deploy') {
      steps {
        echo 'deploying...'
      }
    }
    stage('QA e2e Tests') {
      steps {
        echo 'Capybara testing...'
      }
    }
    stage('Production Deploy') {
      steps {
        echo 'deploying...'
      }
    }
    stage('Production e2e Tests') {
      steps {
        echo 'Capybara testing...'
      }
    }
  }
  post {
    always {
      echo 'Pipeline has finished.'
    }
    success {
      echo 'No errors detected!'
      echo 'Notifying commits authors...'
    }
    failure {
      echo 'Errors detected. Notifying pager duty...'
      echo 'Sending PagerDuty notifications...'
      echo 'Notifying commits authors...'
    }
    unstable {
      echo 'Unstable build.'
    }
    changed {
      echo 'Pipeline state changed!'
      echo 'Was failing but it is now successful'
    }
  }
}

