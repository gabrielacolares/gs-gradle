pipeline {
    agent any
    post {
            always {
                echo 'One way or another, I have finished'
                deleteDir() /* clean up our workspace */
            }
            success {
                echo 'I succeeeded!'
            }
            unstable {
                echo 'I am unstable :/'
            }
            failure {
                echo 'I failed :('
                mail to: 'gcrodrigues@uolinc.com',
                             subject: "Failed Pipeline: ${currentBuild.fullDisplayName}",
                             body: "Something is wrong with ${env.BUILD_URL}"
            }
            changed {
                echo 'Things were different before...'
            }
        }
    stages {
        stage('Deploy') {
            steps {
                retry(3) {
                sh 'echo "Passo 1"'
                    sh 'gradle'
                }
            }
        }
    }
}