pipeline {
    agent any

    stages {
        stage('Checkout Code') {
            steps {
                git branch: 'main', url: 'https://github.com/ashishkongari/web-app.git'
            }
        }

        stage('Build') {
            steps {
                sh 'echo "Building the project..."'
            }
        }

        stage('Deploy') {
            steps {
                sh '''
                echo "Deploying to web server..."
                sudo systemctl stop apache2
                sudo rm -rf /var/www/html/*
                sudo cp -r * /var/www/html/
                sudo systemctl start apache2
                '''
            }
        }
    }
}
