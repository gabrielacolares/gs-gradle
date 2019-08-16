pipeline {
    agent any
    environment {
    BRANCH_DEV = 'dev'
    BRANCH_MASTER = 'master'
    }
    post {
        always {
            echo 'One way or another, I have finished'
            deleteDir() /* clean up our workspace */
        }
        success {
            echo 'I succeeeded!'
//                 fail to: 'gcrodrigues@uolinc.com',
//                                              subject: "succeeeded Pipeline: ${currentBuild.fullDisplayName}",
//                                              body: "succeeeded with ${env.BUILD_URL}"
        }
        unstable {
           echo 'I am unstable :/'
        }
        failure {
            echo 'I failed :('
//                 mail to: 'gcrodrigues@uolinc.com',
//                              subject: "Failed Pipeline: ${currentBuild.fullDisplayName}",
//                              body: "Something is wrong with ${env.BUILD_URL}"
        }
        changed {
            echo 'Things were different before...'
        }
        always {
            unit 'build/reports/**/*.xml'
        }
    }
    stages {
        stage('Build') {
            when {
                branch 'dev'
            }
            steps {
                retry(3) {
                    sh 'echo "Passo 1 na dev"'
                    sh 'gradle'
                }
            }
        }
        stage('Test') {
            steps {
                retry(3) {
                   sh 'echo "Passo 2"'
                }
             }
         }
        stage('Deploy in dev') {
            when {
            branch 'dev'
            }
            steps {
                sh 'echo "Deploy na dev"'
            }
        }
        stage('Deploy in master') {
            steps {
                input "Yes or No?"
                sh 'echo "Deploy na master"'
            }
        }
    }
}