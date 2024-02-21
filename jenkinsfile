pipeline {
    agent any

    tools {
        nodejs "node"
    }

    stages {
        stage('Clone and Build') {
            steps {
                dir('/var/lib/jenkins/workspace/test') {
                    git branch: 'main', url: 'https://github.com/Venkatesh101997/node1.git'
                    //sh 'cp /root/.env /root/var/lib/jenkins/workspace/test'
                    sh 'npm install'
                }
            }
        }

        stage('Run Application') {
            steps {
                script {
                    dir('/var/lib/jenkins/workspace/test') {
                        // Start the application with pm2
                        sh 'pm2 delete all || true'  // Ignore errors if no processes are found
                        sh 'pm2 start /var/lib/jenkins/workspace/test/bin/www --name "erie-path" -l pm2.log > pm2_output.log 2>&1'
                        // Print the contents of the PM2 log to the console
                        sh 'cat pm2.log'
                    }
                }
            }
        }
    }

    post {
        success {
            script {
                echo 'Build succeeded! Access your application at http://13.232.95.79'
            }
        }
        failure {
            script {
                echo 'Build failed! Check the Jenkins logs for details.'
            }
        }
    }
}
