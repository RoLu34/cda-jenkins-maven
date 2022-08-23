pipeline {
    agent any
    tools {
        maven 'maven386'
    }

    stages {
        stage('git'){
            steps{
                git url: 'https://github.com/RoLu34/cda-jenkins-maven.git', branch:'preprod'
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
}