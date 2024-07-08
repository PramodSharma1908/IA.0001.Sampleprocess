pipeline {
    agent any
    triggers {
        // Polling SCM to check for changes, you can also configure a webhook for better efficiency.
        pollSCM('H/5 * * * *')
    }
    environment {
        GIT_COMMIT = sh(script: 'git rev-parse HEAD', returnStdout: true).trim()
        GIT_AUTHOR = sh(script: 'git show -s --format=%an HEAD', returnStdout: true).trim()
        GIT_MESSAGE = sh(script: 'git log -1 --pretty=%B', returnStdout: true).trim()
    }
    stages {
        stage('Checkout') {
            steps {
                // Checkout the code
                git url: 'https://your-git-repo-url.git', branch: 'main'
            }
        }
        stage('Get Commit Details') {
            steps {
                script {
                    // Print commit details
                    echo "Commit ID: ${env.GIT_COMMIT}"
                    echo "Author: ${env.GIT_AUTHOR}"
                    echo "Message: ${env.GIT_MESSAGE}"
                }
            }
        }
    }
    post {
        always {
            // Send notifications or perform cleanup
            echo 'Pipeline completed.'
        }
    }
}
