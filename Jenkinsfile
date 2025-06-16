pipeline {
    agent any

    options {
        timestamps()
    }

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Build') {
            steps {
                script {
                    if (isUnix()) {
                        sh 'echo "Building on ${NODE_NAME}" && make'
                    } else {
                        bat 'echo "Building on %NODE_NAME%" && build.bat'
                    }
                }
            }
        }

        stage('Test') {
            steps {
                script {
                    if (isUnix()) {
                        sh 'echo "Testing on ${NODE_NAME}" && make test'
                    } else {
                        bat 'echo "Testing on %NODE_NAME%" && test.bat'
                    }
                }
            }
        }
    }

    post {
        always {
            echo "Build completed on ${NODE_NAME}"
            archiveArtifacts artifacts: '**/target/*.jar', fingerprint: true
        }
        success {
            echo "Build succeeded!"
        }
        failure {
            echo "Build failed!"
        }
    }
}
