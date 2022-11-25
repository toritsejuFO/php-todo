pipeline {
  agent any

  stages {
    stage("Initial cleanup") {
        steps {
          dir("${WORKSPACE}") {
            deleteDir()
          }
        }
      }

    stage('Checkout SCM') {
      steps {
            git branch: '$BRANCH_NAME', url: 'https://github.com/toritsejuFO/php-todo.git'
      }
    }

    stage('Prepare Dependencies') {
      steps {
        sh 'mv .env.sample .env'
        sh 'composer install'
        sh 'php artisan migrate'
        sh 'php artisan db:seed'
        sh 'php artisan key:generate'
      }
    }

    stage('Execute Unit Tests') {
      steps {
        sh './vendor/bin/phpunit'
      }
    }
  }
}
