pipeline {
    agent any
    stages {
        stage('Deploy') {
            steps {
                retry(3) {
                sh 'echo 'Passo 1''
                    sh 'pwd'
                }
            }
        }
    }
}