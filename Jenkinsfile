pipeline {
    agent { label 'LaravelAgent' } // should be your Linux node label

    environment {
        WORKSPACE = '/home/jenkins/agent/workspace/Laravel-tp03'
    }

    stages {
        stage('Build') {
            steps {
                echo 'Building...'
                checkout scm
                sh 'cp .env.example .env'
                sh 'composer install'
                sh 'npm install'
                sh 'php artisan key:generate'
            }
        }
        stage('Test') {
            steps {
                sh 'php artisan test'
            }
        }
        stage('Deploy') {
            steps {
                sh 'ansible-playbook -i inventory/hosts.ini deploy.yml'
            }
        }
    }
}
