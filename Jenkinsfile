pipeline {
    agent any
    post {
            always {
                echo 'One way or another, I have finished'
                deleteDir() /* clean up our workspace */
            }
            success {
                echo 'I succeeeded!'
                ail to: 'gcrodrigues@uolinc.com',
                                             subject: "succeeeded Pipeline: ${currentBuild.fullDisplayName}",
                                             body: "succeeeded with ${env.BUILD_URL}"
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
            when {
                branch 'dev'
            }
            steps {
                retry(3) {
                    sh 'echo "Passo 1 na dev"'
                    sh 'gradle'
                }
            }
            when {
                branch 'master'
            }
            steps {
                sh 'echo Passo 1 na master'
            }

        }
        stage('Test') {
            steps {
                retry(3) {
                   sh 'echo "Passo 2"'
                }
             }
         }
        stage('Deploy') {
            steps {
                input "Yes or No?"
            }
        }
   }
}