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
                # If you have a build step, add it here
                # e.g., npm install, mvn clean package, etc.
            }
        }

        stage('Deploy') {
            steps {
                sshagent (credentials: ['server-ssh-key']) {
                    sh '''
                    ssh -o StrictHostKeyChecking=no ce00132521@10.10.21.137 "sudo systemctl stop apache2"
                    scp -o StrictHostKeyChecking=no -r * ce00132521@10.10.21.137:/var/www/html/
                    ssh -o StrictHostKeyChecking=no ce00132521@10.10.21.137 "sudo systemctl start apache2"
                    '''
                }
            }
        }
    }
}
