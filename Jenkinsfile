pipeline {
    agent any

    stages {
        stage('Checkout Code') {
            steps {
                echo "===== BUILD #${env.BUILD_NUMBER} STARTED ====="
                script {
                    def currentTime = new Date().format("yyyy-MM-dd HH:mm:ss", TimeZone.getTimeZone('UTC'))
                    echo "Triggered at: ${currentTime} UTC"

                    // Script-security prevents calling `getCauses()` in the sandbox.
                    // Use environment heuristics instead. If you need exact cause detection,
                    // ask an administrator to approve the use of `getCauses()` in Script Approval.
                    def triggeredBySCM = (env.GIT_COMMIT != null && env.GIT_COMMIT != '')
                    if (triggeredBySCM) {
                        echo "Triggered by SCM change (commit/webhook) ✅"
                    } else {
                        echo "Triggered manually or unknown 🖐️"
                    }
                }

                // Use the repository for this project
                git branch: 'main', url: 'https://github.com/itsalihamza/Jenkins_Task-3.git'
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

