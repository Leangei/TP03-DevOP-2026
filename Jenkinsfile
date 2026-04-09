pipeline {
    agent { label 'LaravelAgent' }  // Only one agent specification here

    environment {
        WORKSPACE = '/home/jenkins/agent/workspace/Laravel-tp03'
    }

    stages {
        stage('Build') {
            steps {
                echo 'Building...'
                checkout scm

                // Use Git tool if needed
                tool name: 'LinuxGit', type: 'Git'

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
