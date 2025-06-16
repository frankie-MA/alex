pipeline {
    agent {
        label 'node1 || node2' // Использует любой доступный агент
    }

    stages {
        stage('Build') {
            steps {
                sh 'make --version'
                sh 'git --version'
            }
        }
    }
}
