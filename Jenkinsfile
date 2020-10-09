pipeline {
    agent any

    stages {
        stage('UnitTest') {
            steps {
               sh 'chmod +x rununittest.sh; ./rununittest.sh'
            }
        }
        stage('Build') {
            steps {
                sh 'chmod +x buildapp.sh;./buildapp.sh'
            }
        }
        stage('Deploy') {
            steps {
                sh 'chmod +x deployapp.sh; ./deployapp.sh'
            }
        }
    }
    post {
        failure {
            mail bcc: '', body: "<b>gopro build failed</b><br>Project: ${env.JOB_NAME} <br>Build Number: ${env.BUILD_NUMBER} <br> URL de build: ${env.BUILD_URL}", cc: '', charset    : 'UTF-8', from: 'yunwei-monitor@donews.com', mimeType: 'text/html', replyTo: '', subject: "ERROR CI: Project name -> ${env.JOB_NAME}", to: "mawencheng@donews.com";
        }
        success {
            emailext (
                        to: 'mawencheng@donews.com',
                        subject: "${currentBuild.currentResult}: ${env.JOB_NAME} - build ${currentBuild.number}",
                        body: '${FILE, path="root/.jenkins/workspace/marvin-test/coverage.html"}'
                    )
        }
    }
}