pipeline {
    agent any

    environment {
        NODEJS_HOME = tool name: 'NodeJS', type: 'NodeJSInstallation'
        PATH = "${NODEJS_HOME}/bin:${env.PATH}"
    }

    stages {
        stage('Clone Repository') {
            steps {
                git 'https://github.com/faizrahmang/DEVOPs.git'
            }
        }
        
        stage('Install Dependencies') {
            steps {
                sh 'npm install'
            }
        }

        stage('Run Tests') {
            steps {
                // Add your test command here, e.g., npm test
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
                
                // Ensure that Jenkins can SSH into your AWS Ubuntu instance.
                // This will copy your application to the /var/www/myapp directory on your AWS Ubuntu server.
                // Replace "ubuntu" with the correct username, typically "ubuntu" for AWS EC2 Ubuntu AMIs.

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