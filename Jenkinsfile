// pipeline {
//    agent any
//    stages {
//     stage('Test Message') {
//        echo 'Hello World'
//     }
//    }
// }
pipeline {
    agent any

    stages {
        stage('Checkout Code') {
            steps {
                git https://github.com/Ros7979/StudentRegistryAppDocker.git
            }
        }

        stage('Set Up Node.js') {
            steps {
                script {
                    // Use Node.js version specified in the environment
                    def nodeVersion = '20.x'
                    env.NODE_HOME = tool name: 'NodeJS', type: 'NodeJSInstallation'
                    sh """
                        curl -sL https://deb.nodesource.com/setup_${nodeVersion}.x | sudo -E bash -
                        sudo apt-get install -y nodejs
                    """
                }
            }
        }

        stage('Install Dependencies') {
            steps {
                sh 'npm install'
            }
        }

        stage('Start Application') {
            steps {
                // This is just an example, adjust based on your application
                sh 'npm start &'
            }
        }

        stage('Run Tests') {
            steps {
                sh 'npm test'
            }
        }
    }

    post {
        always {
            // Clean up or perform actions regardless of the build result
            sh 'kill $(lsof -t -i:8081)' // Adjust port based on your app
        }
        success {
            echo 'Build succeeded!'
        }
        failure {
            echo 'Build failed!'
        }
    }
}
