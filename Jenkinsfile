pipeline {
    agent any

    stages {
        stage('Checkout Code') {
            steps {
                echo "===== BUILD #${env.BUILD_NUMBER} STARTED ====="
                script {
                    def currentTime = new Date().format("yyyy-MM-dd HH:mm:ss", TimeZone.getTimeZone('UTC'))
                    echo "Triggered at: ${currentTime} UTC"

                    if (currentBuild.rawBuild.getCauses().toString().contains("Push event")) {
                        echo "Triggered by GitHub Webhook ✅"
                    } else {
                        echo "Triggered manually 🖐️"
                    }
                }

                git branch: 'main', url: 'https://github.com/noorulain-nn/task.git'
            }
        }

        stage('Install Dependencies') {
            steps {
                bat 'npm install'
            }
        }

        stage('Run Tests') {
            steps {
                bat 'npm test'
            }
        }
    }

    post {
        success {
            echo "Build #${env.BUILD_NUMBER} completed successfully ✅"
        }
        failure {
            echo "Build #${env.BUILD_NUMBER} failed ❌"
        }
    }
}

