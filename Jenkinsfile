pipeline {
    agent any
    stages {
        stage('Deploy') {
            steps {
                retry(3) {
                    sh 'cd /test'
                    sh './run.sh'
                }
            }
        }
    }
}