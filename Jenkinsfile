pipeline {
    agent any
    tools {
        maven 'maven386'
    }

    stages {
        stage('git'){
            steps{
                echo 'git...'
                git url: 'https://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@github.com/RoLu34/cda-jenkins-maven.git', branch: 'preprod'
            }
        }
        stage('build') {
            steps {
                echo 'Building...'
                build('preprod')
            }
        }
        stage('test') {
            steps {
                echo 'Testing...'
                sh 'mvn test'
            }
        }
        stage('deploy') {
            steps {
                echo 'Deployment...'
                sh 'git checkout main'
                sh 'git merge preprod'
                sh 'git push origin main'
                echo 'Deployment OK'
            }
        }
    }
    post {
        always {
            echo "Release finished do cleanup and send mails"
            deleteDir()
        }
        success {
            echo "Release Success"
        }
        failure {
            echo "Release Failed"
        }
        cleanup {
            echo "Clean up in post work space"
            cleanWs()
        }
    }
}