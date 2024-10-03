pipeline {
    agent any

    environment {
        NODEJS_HOME = tool name: 'NodeJS_LTS', type: 'NodeJSInstallation'
        PATH = "${NODEJS_HOME}/bin:${env.PATH}"
    }

    stages {
        stage('Clone Repository') {
            steps {
                git 'https://github.com/faizrahmang/DEVOPs.git'
            }
        }

        stage('Check Node Version') {
            steps {
                sh 'node -v' // Check if Node.js is properly installed
            }
        }

        stage('Install Dependencies') {
            steps {
                sh 'npm install'
            }
        }

        stage('Run Tests') {
            steps {
                echo 'Running Tests...'
            }
        }

        stage('Build') {
            steps {
                echo 'Building the application...'
                sh 'npm run build' // If your project has a build step
            }
        }

        stage('Deploy to AWS Ubuntu Server') {
            steps {
                echo 'Deploying application to AWS Ubuntu server...'
                sh '''
                scp -o StrictHostKeyChecking=no -r ./ ubuntu@54.161.154.161:/var/www/myapp
                ssh ubuntu@54.161.154.161 'pm2 restart myapp || pm2 start /var/www/myapp/index.js --name myapp'
                '''
            }
        }
    }

    post {
        success {
            echo 'Pipeline succeeded!'
        }
        failure {
            echo 'Pipeline failed!'
        }
    }
}
