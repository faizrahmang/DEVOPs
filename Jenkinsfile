pipeline {
    agent any

    environment {
        NODEJS_HOME = tool name: 'NodeJS', type: 'NodeJSInstallation'
        PATH = "${NODEJS_HOME}/bin:${env.PATH}"
    }

    stages {
        stage('Clone Repository') {
            steps {
                git 'https://github.com/your-username/ci-cd-sample-app.git'
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

        stage('Deploy') {
            steps {
                echo 'Deploying application...'
                sh 'scp -r ./ your-server-user@your-server-ip:/path/to/deploy'
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